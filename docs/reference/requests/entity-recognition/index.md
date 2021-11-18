# Named entity recognition requests

The JSON object that constitutes the payload of requests for [named entity recognition](../../../guide/entity-recognition/index.md) varies based on essex [execution mode](../../../setup-execution/index.md#execution) and must be like this:

=== "Single resource mode"
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
=== "Server mode"
	``` json
	{
		"resource": "Resource name here",
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
