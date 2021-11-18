# Self-documentation resources requests

## Categories' tree

The JSON object that constitutes the payload of the request for the [categories' tree](../../../guide/categories-tree/index.md) self-documentation resource varies based on essex [execution mode](../../../setup-run/index.md#execution) and must be like this:

=== "Single resource mode"
	``` json
	{
		"info": "taxonomy"
	}
	```
=== "Server mode"
	``` json
	{
		"resource": "Resource name here",
		"info": "taxonomy"
	}
	```

## Templates

The JSON object that constitutes the payload of the request for [information extraction templates](../../../guide/templates/index.md) self-documentation resource varies based on essex [execution mode](../../../setup-run/index.md#execution) and must be like this:

=== "Single resource mode"
	``` json
	{
		"info": "templates"
	}
	```
=== "Server mode"
	``` json
	{
		"resource": "Resource name here",
		"info": "templates"
	}
	```