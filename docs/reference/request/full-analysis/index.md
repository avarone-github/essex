# Full document analysis request

The JSON object that constitutes the payload of requests for the [full document analysis](../../../guide/full-analysis/index.md) API resource must have this structure:

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
	
For the description of the `options`, read the [overview](../index.md) article.