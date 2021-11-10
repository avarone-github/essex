# Named entity recognition requests

The JSON object that constitutes the payload of requests for [named entity recognition](../../../guide/entity-recognition/index.md) must be like this:

``` json
{
	"document": {
		"text": "Your text here."
	},
	"options": {
		"analysis": [
			"entities"
		],
		"features": [
			"knowledge",
			"dependency",
			"syncpos"
		]
	}
}
```