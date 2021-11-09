# Sentiment analysis output

The [sentiment analysis](../../../guide/sentiment-analysis/index.md) resource returns a JSON object with this format:

<pre>
<code>{
	"success": <i>Boolean success flag</i>,
	"data": {
		"content": <i>analyzed text</i>,
		"language": <i>language code</i>,
		"version": <i>technology version info</i>,
		<strong>"knowledge": [],
		"sentiment": []</strong>
	}
}</code></pre>

For the description of the `contents`, `language` and `version` properties, see the API resources output [overview](../index.md).

The `knowledge` array contains [Knowledge Graph](../../../guide/knowledgegraph/index.md) data about items of the `sentiment` array, as a result of the [semantic analysis](../../../guide/linguistic-analysis/semantic-analysis/index.md) process. Its contents are described in the article about the output of [full analysis](../full-analysis/index.md#knowledge).

## sentiment

The `sentiment` object contains three scores indicative of the tone of the whole text:

- `positivity`: the amount of positivity
- `negativity`: the amount of negativity
- `overall`: the overall sentiment score, which is a combination of the scores above

All sentiment scores are expressed in a -100 (extremely negative) to 100 (extremely positive) range.

The `sentiment` object contains an `items` array whose elements, in turn, can contain nested `items` arrays. These items represent the clusters of text elements that give a positive or negative contribution to sentiment.

For example, given this input text:

    The road was bad.
    
items clusters can be like this:

``` json
"items": [
	{
		"lemma": "road",
		"sentiment": -7,
		"syncon": 19001,
		"items": [
			{
				"lemma": "bad",
				"sentiment": -7,
				"syncon": 81195
			}
		]
	}
]
```

`sentiment` is the sentiment score of the cluster or leaf-item. The sentiment score of a cluster is a function of the child items' scores and the the possible modifiers, which are not returned as separate item, but are nevertheless taken into account.  

Take, for example, a slight change introduced in the sample text:

    The road was really bad.

the _really_ modifier makes the score get worse:

``` json hl_lines="4 9"
"items": [
	{
		"lemma": "road",
		"sentiment": -8.8,
		"syncon": 19001,
		"items": [
			{
				"lemma": "bad",
				"sentiment": -8.8,
				"syncon": 81195
			}
		]
	}
]

On the other hand, a _not_ before _bad_ can invert the sentiment polarity from negative to positive. The sentiment value can be zero.

The `syncon` and `lemma` properties are the outcome of semantic analysis and lemmatization respectively. These are the same processes carried out during [deep linguistic analysis](../../../guide/linguistic-analysis/index.md), but the value of `lemma` can have some peculiarities.  
An item having nested items can be an "unnamed cluster": in that case the `lemma` property is an empty string.  
If the intrinsic item polarity&mdash;positive or negative&mdash;is opposite of that of the paragraph it belongs to, this marker:

    [*]

is added as a suffix to the the lemma.  
For example, given this input text:

    The road was not bad.

The lemma for _bad_ is marked with the "opposite polarity" sign because it is negated by _not_:

``` json hl_lines="5"
"items": [
	{
		"items": [
			{
				"lemma": "bad[*]",
				"sentiment": 7,
				"syncon": 87597
			}
		],
		"lemma": "road",
		"sentiment": 7,
		"syncon": 19001
	}
]
```

Another possibility is that a lemma "attracts" other words in the same phrase. For example, given the input text:

    Michael Jordan was one of the best basketball players of all time. Scoring was Jordan's stand-out skill, but he still holds a defensive NBA record, with eight steals in a half.
    
a value of `lemma` could be:

    stand-out;skill

In this case the merged terms are separated by a semi-colon (`;`).

Value -1 for `syncon` means the concept doesn't have a correspondent in the expert.ai [Knowledge Graph](../../../guide/knowledgegraph/index.md).

## knowledge

The `knowledge` array contains [Knowledge Graph](../../../guide/knowledgegraph/index.md) data for the elements of the `items` array. Its contents are described in the article about the output of [full analysis](../full-analysis/index.md#knowledge).