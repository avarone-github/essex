# Document classification output

The [document classification](../../../guide/classification/index.md) resource returns a JSON object with this format:

<pre>
<code>{
	"success": <i>Boolean success flag</i>,
	"data": {
		"content": <i>analyzed text</i>,
		"language": <i>language code</i>,
		"version": <i>technology version info</i>,
		<strong>"categories": []</strong>
	}
}</code></pre>

For the description of the `contents`, `language` and `version` properties, see output [overview](../index.md).

Each item of the `categories` array represents a category, for example:

``` json
{
	"frequency": 70.62,
	"hierarchy": [
		"Sport",
		"Competition discipline",
		"Basketball"
	],
	"id": "20000851",
	"label": "Basketball",
	"namespace": "iptc_en_1.0",
	"positions": [
		{
			"end": 14,
			"start": 0
		},
		{
			"end": 53,
			"start": 35
		},
		{
			"end": 139,
			"start": 136
		}
	],
	"score": 4005.0,
	"winner": true
}
```

- `namespace` is the name of the software module carrying out document classification.
- `id`, `label` and `hierarchy` identify the category in the [categories' tree](../taxonomies-templates/index.md).  
- `score` is the cumulative score that was attributed to the category.
- `frequency` is the percentage ratio of the category score to the sum of all categories' scores.
- `winner` is a Boolean flag set to `true` if the category was considered particularly relevant.
- `positions` is an array containing the [positions](../../positions/index.md) of the text blocks that contributed to category score.