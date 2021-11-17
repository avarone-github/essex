# Information exraction output

The [information extraction](../../../guide/extraction/index.md) resource returns a JSON object with this format:

<pre>
<code>{
	"success": <i>Boolean success flag</i>,
	"data": {
		"content": <i>analyzed text</i>,
		"language": <i>language code</i>,
		"version": <i>technology version info</i>,
		<strong>"extractions": []</strong>
	}
}</code></pre>

For the description of the `contents`, `language` and `version` properties, see output [overview](../index.md).

Each item of the `extractions` array represents an extraction record, for example:

``` json
"extractions": [
	{
		"namespace": "project01",
		"template": "RELATIONS",
		"fields": [
			{
				"name": "DISEASE",
				"value": "Diabetes",
				"positions": [
					{
						"start": 1621,
						"end": 1629
					}
				]
			},
			{
				"name": "DISEASE2",
				"value": "COVID-19",
				"positions": [
					{
						"start": 1673,
						"end": 1684
					}
				]
			},
			{
				"name": "RELATION",
				"value": "TR_RISK_FACTOR",
				"positions": [
					{
						"start": 1642,
						"end": 1656
					}
				]
			}
		]
	}
]
```

- `namespace` is the name of the software module carrying out information extraction inside the text intelligence engine.
- `template` is the name of the record's template 
- `fields` is the array of record's fields.

Each item of the `fields` array represents an extracted field, where:

- `name` is the field's name.
- `value` is the field's value.
- `positions` is an array containing the extracted field's [positions](../../positions/index.md).

!!! info
	You can find more information about templates and fields in the	<a href="https://docs.expert.ai/studio/latest/languages/extraction/structures/" target="_blank">Studio documentation</a>.