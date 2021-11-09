# Deep linguistic analysis output

The [deep linguistic analysis](../../../guide/linguistic-analysis/index.md) resource returns a JSON object with this format:

<pre>
<code>{
	"success": <i>Boolean success flag</i>,
	"data": {
		"content": <i>analyzed text</i>,
		"language": <i>language code</i>,
		"version": <i>technology version info</i>,
		<strong>"knowledge": [],
		"tokens": [],
		"phrases": [],
		"sentences": [],
		"paragraphs": []</strong>
	}
}</code></pre>

For the description of the `contents`, `language` and `version` properties, see the API resources output [overview](../index.md).

The `knowledge` array contains [Knowledge Graph](../../../guide/knowledgegraph/index.md) data as a result of the [semantic analysis](../../../guide/linguistic-analysis/semantic-analysis/index.md) process. Its contents are described in the article about the output of [full analysis](../full-analysis/index.md#knowledge).

The `paragraphs`, `sentences`, `phrases` and `tokens` arrays are produced by the [text subdivision process](../../../guide/linguistic-analysis/subdivision/index.md).  
The items of the `tokens` array are then enriched by the other deep linguistic analysis processes: [part-of-speech tagging](../../../guide/linguistic-analysis/pos-tagging/index.md), [morphological analysis](../../../guide/linguistic-analysis/morphological-analysis/index.md), [lemmatization](../../../guide/linguistic-analysis/lemmatization/index.md), [syntactic analysis](../../../guide/linguistic-analysis/syntactic-analysis/index.md) and [semantic analysis](../../../guide/linguistic-analysis/semantic-analysis/index.md).  
The contents of these arrays are described below.

## tokens

The `tokens` array contains an item for every token detected. Each item has a format like this:

``` json
{
	"syncon": 62653,
	"start": 74,
	"end": 83,
	"type": "NOU",
	"lemma": "long time",
	"pos": "NOUN",
	"dependency": {
		"id": 11,
		"head": 7,
		"label": "nmod"
	},
	"morphology": "Number=Sing",
	"paragraph": 0,
	"sentence": 0,
	"phrase": 4,
	"atoms": [
		{
			"start": 74,
			"end": 78,
			"type": "ADJ",
			"lemma": "long"
		},
		{
			"start": 79,
			"end": 83,
			"type": "NOU",
			"lemma": "time"
		}
	]
}	
```

- The `syncon` property is the outcome of the [semantic analysis](../../../guide/linguistic-analysis/semantic-analysis/index.md) process. Its value is the ID of the corresponding syncon in the Knowledge Graph. The -1 value is attributed to tokens that do not have a corresponding syncon. A positive value has a match in the value of the `syncon` property of an entry in the [`knowledge`](#knowledge) array.
- `type` is the result of custom [part-of-speech tagging](../../../guide/linguistic-analysis/pos-tagging/index.md).
- `lemma` is the result of [lemmatization](../../../guide/linguistic-analysis/lemmatization/index.md).
- `pos` is the result of standard [part-of-speech tagging](../../../guide/linguistic-analysis/pos-tagging/index.md).
- `dependency` is the result of [syntactic analysis](../../../guide/linguistic-analysis/syntactic-analysis/index.md).
	- `id` represents the index of the token in the text.
	- `dep` specifies the dependency relation with another token according to the <a href="https://universaldependencies.org/u/dep/index.html" target="_blank">Universal Dependencies conventions</a>.  
	- `head` identifies the token that _receives_ the relation the relation. Its value corresponds to the value of the `id` property of another token, the only exception being the _root token_&mdash;the one with the `dep`property set to `root`&mdash;for which `head` and `id` have the same value.
- `morphology` is the result of [morphological analysis](../../../guide/linguistic-analysis/morphological-analysis/index.md).
- `start`, `end`, `phrase`, `sentence` and `paragraph` are the result of [text subdivision process](../../../guide/linguistic-analysis/subdivision/index.md).
	- `start` and `end` are the [positions](../../positions/index.md) of the token text in the analyzed text, which is the value of the `content` property of the outer `data` object.
	- `phrase` is the phrase containing the token; it's the zero-based index of the phrase in the `phrases` array.
	- `sentence` is the sentence containing the token; it's the zero-based index of the sentence in the `sentences` array.
	- `paragraph` is the paragraph containing the token; it's the zero-based index of the paragraph in the `paragraphs` array.
	
In the case of collocations, the token object can contain the `atoms` array. There's an item for every word of the collocation in the atoms array and in each item of the `atoms` array:

- `start` and `end` are the result of [text subdivision process](../../../guide/linguistic-analysis/subdivision/index.md). They represent the [positions](../../positions/index.md) of the atom text in the analyzed text, which is the value of the `content` property of the outer `data` object 
- `type` is the the result of custom [part-of-speech tagging](../../../guide/linguistic-analysis/pos-tagging/index.md).
- `lemma` property is the result of [lemmatization](../../../guide/linguistic-analysis/lemmatization/index.md) for to the word.

Sometimes the [semantic analysis](../../../guide/linguistic-analysis/semantic-analysis/index.md) process determines that a token is a named entity&mdash;for example: a person's name&mdash;even if there is no corresponding concept in the Knowledge Graph.
In this case the syncon property is set to -1, but the token has an additional `vsyn` property. For example:

``` json hl_lines="3 4 5 6"
{
	"syncon": -1,
	"vsyn": {
		"id": -436106,
		"parent": 73303
	},
	"start": 0,
	"end": 19,
	"type": "NPR.NPH",
	"lemma": "Mauricio Pochettino",
	...
```

This property, whose name means "virtual syncon", is an object with two properties:

- `id` is a negative number generated by the semantic analysis process and assigned to all tokens considered as occurrences of the same entity. It is not the ID of a Knowledge Graph syncon.
- `parent` is the number of a Knowledge Graph syncon which, conceptually, is the _parent_ of the concept expressed by the token. For example, if the token has been recognized as a person's name, its parent is the concept of _person_. The parent syncon data is located in the `knowledge` array.

## phrases

The `phrases` array is created and populated by the [text subdivision](../../../guide/linguistic-analysis/subdivision/index.md) process.
It contains an item for every phrase detected. For example, the phrase:

<pre>
<code>
Michael Jordan was one of the best basketball players <span class="bordered">of all time</span>.
</code>
</pre>
	
corresponds to an array item like this:

``` json
{
	"tokens": [
		7,
		8,
		9
	],
	"type": "PP",
	"start": 54,
	"end": 65
}
```

The `tokens` array contains the zero-based indexes of the constituent tokens. For example, token `7` is the 8th token.
`type` specifies the [phrase type](../../phrase-types/index.md).
`start` and `end` are the [positions](../../positions/index.md) of the phrase in the analyzed text, which is the value of the `content` property of the outer `data` object.

## sentences

The `sentences` array is created and populated by the [text subdivision](../../../guide/linguistic-analysis/subdivision/index.md) process.
It contains an item for every sentence detected. For example, this sentence:

	Michael Jordan was one of the best basketball players of all time.
	
corresponds to an array item like this:

``` json
{
	"phrases": [
		0,
		1,
		2,
		3,
		4,
		5
	],
	"start": 0,
	"end": 66
}
```

The `phrases` array contains the zero-based indexes of the constituent phrases.
`start` and `end` are the [positions](../../positions/index.md) of the sentence in the analyzed text, which is the value of the `content` property of the outer `data` object.

## paragraphs

The `paragraphs` array is created and populated by the [text subdivision](../../../guide/linguistic-analysis/subdivision/index.md) process.
It contains an item for every paragraph detected. For example this text:

	Michael Jordan was one of the best basketball players of all time. Scoring was Jordan's stand-out skill, but he still holds a defensive NBA record, with eight steals in a half.
	
	Michael Jordan was also a baseball player and an actor.

contains two paragraphs and the corresponding array is something like:
	
``` json
"paragraphs": [
	{
		"sentences": [
			0,
			1
		],
		"start": 0,
		"end": 176
	},
	{
		"sentences": [
			2
		],
		"start": 177,
		"end": 232
	}
]
```

The `sentences` array in each item contains the zero-based indexes of the constituent sentences.
`start` and `end` are the [positions](../../positions/index.md) of the paragraph in the analyzed text, which is the value of the `content` property of the outer `data` object.

## knowledge

The `knowledge` array contains [Knowledge Graph](../../../guide/knowledgegraph/index.md) data for the items of the `tokens` array. Its contents are described in the article about the output of [full analysis](../full-analysis/index.md#knowledge).