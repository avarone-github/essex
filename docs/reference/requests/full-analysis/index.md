# Full document analysis requests

The JSON object that constitutes the payload of requests for [full document analysis](../../../guide/full-analysis/index.md) varies based on essex [execution mode](../../../setup-run/index.md#execution) and must be like this:

=== "Single resource mode"
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
=== "Server mode"
	``` json
	{
		"resource": "Resource name here",
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
