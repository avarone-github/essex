# Keyphrase extraction requests

The JSON object that constitutes the payload of requests for [keyphrase extraction](../../../guide/keyphrase-extraction/index.md) must be like this:

``` json
{
	"document": {
		"text": "Your text here."
	},
	"options": {
		"analysis": [
			"relevants"
		],
		"features": [
			"knowledge",
			"dependency",
			"syncpos"
		]
	}
}
```