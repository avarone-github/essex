# Document classification requests

The JSON object that constitutes the payload of requests for [document classification](../../../guide/classification/index.md) varies based on essex [execution mode](../../../setup-execution/index.md#execution) and must be like this:

=== "Single resource mode"
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
=== "Server mode"
	``` json
	{
		"resource": "Resource name here",
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