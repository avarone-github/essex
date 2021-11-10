# Deep linguistic analysis requests

The JSON object that constitutes the payload of requests for [deep linguistic analysis](../../../guide/linguistic-analysis/index.md) must be like this:

``` json
{
	"document": {
		"text": "Your text here."
	},
	"options": {
		"analysis": [
			"disambiguation"
		],
		"features": [
			"knowledge",
			"dependency",
			"syncpos"
		]
	}
}
```