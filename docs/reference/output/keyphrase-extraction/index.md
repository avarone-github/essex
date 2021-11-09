# Keyphrase extraction output

The [keyphrase extraction](../../../guide/keyphrase-extraction/index.md) resource returns a JSON object with this structure:

<pre>
<code>{
	"success": <i>Boolean success flag</i>,
	"data": {
		"content": <i>analyzed text</i>,
		"language": <i>language code</i>,
		"version": <i>technology version info</i>,		
		<strong>"knowledge": [],
		"topics": [],
		"mainSentences": [],
		"mainPhrases": [],
		"mainSyncons": [],
		"mainLemmas": []</strong>
	}
}</code></pre>

For the description of the `contents`, `language` and `version` properties see the API resources output [overview](../index.md).

## Common properties

Items that can be directly mapped to the text have properties indicating their [position](../../positions/index.md).  
Items that occur only once, such as a sentence, have a `start` and `end` properties while items that can occur multiple times, such as a main lemma, have a `positions` array containing the start and end positions of all the occurrences.

Items also have a `score` property which provides a measure of their relevance.

## topics

The `topics` array contains references to [Knowledge Graph](../../../guide/knowledgegraph/index.md) topics pertinent with the text.  
Each array item corresponds to a topic, for example:

``` json
{
	"id": 223,
	"label": "mechanics",
	"score": 3.5,
	"winner": true
}
```

Possible topics are listed in the [reference section](../../topics/index.md).  
`id` is the identification number, `winner` is a Boolean flag set to true if the topic is considered particularly relevant.

## mainSentences

The `mainSentences` array contains info about relevant sentences.  
Each array item represents a sentence, for example:

``` json
{
	"value": "The machine is held until ready to start by a sort of trap to be sprung when all is ready; then with a tremendous flapping and snapping of the four-cylinder engine, the huge machine springs aloft.",
	"score": 13.3,
	"start": 740,
	"end": 936
}
```

## mainPhrases

The `mainPhrases` array contains info about the phrases deemed particularly representative during the analysis.  
Each array item represents a phrase, for example:

``` json
{
	"value": "four-cylinder engine",
	"score": 8,
	"positions": [
		{
			"start": 883,
			"end": 903
		}
	]
}
```

## mainSyncons

The `mainSyncons` array contains references to Knowledge Graph syncons corresponding to the concepts that were considered relevant.  
Each array item represents a syncon, for example:

``` json
{
	"lemma": "experiment",
	"positions": [
		{
			"end": 224,
			"start": 213
		},
		{
			"end": 2830,
			"start": 2820
		}
	],
	"score": 5.8,
	"syncon": 2496
}
```

The `syncon` and the `lemma` properties are the outcome of semantic analysis and lemmatization respectively. These are exactly the same processes carried out during [deep linguistic analysis](../../../guide/linguistic-analysis/index.md). `syncon` can be interpreted as a pointer to the [`knowledge`](#knowledge) array entry having its `syncon` property set to the same value.

## mainLemmas
The `mainLemmas` array contains relevant lemmas.  
Each array item represents a lemma, for example:

``` json
{
	"value": "locomotive",
	"score": 6.5,
	"positions": [
		{
			"start": 1152,
			"end": 1162
		},
		{
			"start": 1163,
			"end": 1167
		},
		{
			"start": 1239,
			"end": 1249
		},
		{
			"start": 1335,
			"end": 1345
		},
		{
			"start": 1394,
			"end": 1404
		}
	]
}
```

## knowledge

The `knowledge` array contains [Knowledge Graph](../../../guide/knowledgegraph/index.md) data for the items of the `mainSyncons` array. Its contents are described in the article about the output of [full analysis](../full-analysis/index.md#knowledge).