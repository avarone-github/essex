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

Each item of the `extractions` array represents an extraction record (a template instance), for example:

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

- `namespace` is the name of the software package exported from expert.ai Studio.
- `template` is the name of the template for each extracted data record (Templates and Fields are defined in the expert.ai Studio project, see 
	<a href="https://docs.expert.ai/studio/latest/languages/extraction/structures/">Templates and fields</a> in the Studio documentation).
- `fields` is the list of the extracted fields related to the template (Templates and Fields are defined in the expert.ai Studio project, see 
	<a href="https://docs.expert.ai/studio/latest/languages/extraction/structures/" target="_blank">Templates and fields</a> in the Studio documentation).

Each `fields` array item represents an extracted value, which is related to each other.

- `name` is the field's name.
- `value` is the field's value.
- `positions` is an array containing the extracted field's [positions](../../positions/index.md).

