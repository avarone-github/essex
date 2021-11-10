# Full document analysis requests

The JSON object that constitutes the payload of requests for [full document analysis](../../../guide/full-analysis/index.md) must be like this:

``` json
{
	"document": {
		"text": "Your text here."
	},
	"options": {
		"analysis": [
			"disambiguation",
			"relevants",
			"entities",
			"sentiment",
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