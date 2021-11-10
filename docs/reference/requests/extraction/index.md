# Information extraction requests

The JSON object that constitutes the payload of requests for [information extraction](../../../guide/extraction/index.md) must be like this:

``` json
{
	"document": {
		"text": "Your text here."
	},
	"options": {
		"analysis": [
			"extractions"
		],
		"features": [
			"knowledge",
			"dependency",
			"syncpos"
		]
	}
}
```