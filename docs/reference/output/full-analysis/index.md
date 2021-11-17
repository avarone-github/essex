# Full document analysis output

The [full analysis](../../../guide/full-analysis/index.md) resource returns a JSON object with this format:

<pre>
<code>{
	"success": <i>Boolean success flag</i>,
	"data": {
		"content": <i>analyzed text</i>,
		"language": <i>language code</i>,
		"version": <i>technology version info</i>,
		<strong>"knowledge": [],
		"paragraphs": [],
		"sentences": [],
		"phrases": [],
		"tokens": [],
		"mainSentences": [],
		"mainPhrases": [],
		"mainLemmas": [],
		"mainSyncons": [],
		"topics": [],
		"entities": [],
		"relations": [],		
		"sentiment": {}</strong>
	}
}</code></pre>

For the description of the `contents`, `language` and `version` properties, see the API output [overview](../index.md).

Components arrays have the same structure they have in the response of the resource that performs the corresponding process, so:

- For:
	- `paragraphs`
	- `sentences`
	- `phrases`
	- `tokens`
	
	arrays see the format of [deep linguistic analysis output](../linguistic-analysis/index.md).
	
- For:
	- `mainSentences`
	- `mainPhrases`
	- `mainLemmas`
	- `mainSyncons`
	- `topics`
	
	arrays see the format of [keyphrase extraction output](../keyphrase-extraction/index.md).
	
- For:
	- `entities`
	
	array see the format of [named entity recognition output](../entity-recognition/index.md).
	
- For:
	- `relations`
	
	array see the format of [relation extraction output](../relation-extraction/index.md).

- For:
	- `sentiment`
	
	object see the format of [sentiment analysis output](../sentiment-analysis/index.md).

## knowledge

The `knowledge` array contains [Knowledge Graph](../../../guide/knowledgegraph/index.md) data information about syncons.

Items in these arrays:

- `tokens`
- `manSyncons`
- `entities`
- `relations`
- `items` (in the `sentiment` object)

can have a `syncon` property: the link between those items and the corresponding items in the `knowledge` array is thus represented by the value of the `syncon` property both items have in common.  
For example, if this is an item of the `tokens` array:

``` json hl_lines="29"
{
	"atoms": [
		{
			"end": 45,
			"lemma": "basketball",
			"start": 35,
			"type": "NOU"
		},
		{
			"end": 53,
			"lemma": "player",
			"start": 46,
			"type": "NOU"
		}
	],
	"dependency": {
		"head": 2,
		"id": 6,
		"label": "nmod"
	},
	"end": 53,
	"lemma": "basketball player",
	"morphology": "Number=Plur",
	"paragraph": 0,
	"phrase": 2,
	"pos": "NOUN",
	"sentence": 0,
	"start": 35,
	"syncon": 41583,
	"type": "NOU"
}
```

the corresponding entry in the `knowledge` array can be:

``` json hl_lines="9"
{
	"label": "person.athlete.basketball_player",
	"properties": [
		{
			"type": "WikiDataId",
			"value": "Q3665646"
		}
	],
	"syncon": 41583
}
```
            
It can be a "many-to-one" relationship since more than one item in the `tokens`, `relations` and sentiment `items` arrays can have the same syncon ID, but there's always one entry in the `knowledge` array for a given syncon, so the `knowledge` array is a reference table.  
For example, if a text contains several occurrences of _basketball player_, each occurrence corresponds to a separate item in the `tokens` array, but all tokens "point" to the same entry in the `knowledge` array.

Items with the syncon property set to -1 have no corresponding entry in the `knowledge` array. This is because they are concepts recognized through heuristics and are not present in the Knowledge Graph.

Each entry in the array has a format like this:

``` json
{
	"label": "person",
	"properties": [
		{
			"type": "WikiDataId",
			"value": "Q215627"
		}
	],
	"syncon": 73282
}
```
	
The `label` property is a textual rendering of the general conceptual category for the syncon in the Knowledge Graph.

The `properties` array contains the outcome of knowledge linking. Each item has two properties, `type` and `value`.
`type` specifies the knowledge base, `value` is the property value.
Possible knowledge bases and interpretations of the `value` property follow.

`type` | `value`
--- | ---
`Coordinate` | Latitude and longitude
`WikiDataId` | Wikipedia article ID
`DBpediaId` | URL of the DBPedia content
`GeoNamesId` | ID of the record in the GeoNames database