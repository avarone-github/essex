# Relation extraction requests

The JSON object that constitutes the payload of requests for [relation extraction](../../../guide/relation-extraction/index.md) must be like this:

``` json
{
	"document": {
		"text": "Your text here."
	},
	"options": {
		"analysis": [
			"relations"
		],
		"features": [
			"knowledge",
			"dependency",
			"syncpos"
		]
	}
}
```