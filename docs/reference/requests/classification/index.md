# Document classification requests

The JSON object that constitutes the payload of requests for [document classification](../../../guide/classification/index.md) must be like this:

``` json
{
	"document": {
		"text": "Your text here."
	},
	"options": {
		"analysis": [
			"categories"
		],
		"features": [
			"knowledge",
			"dependency",
			"syncpos"
		]
	}
}
```