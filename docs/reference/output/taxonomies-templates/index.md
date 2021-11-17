# Self-documentation resources output

## Categories' tree

The output of the self-documentation resource returning the [categories' tree](../../../guide/categories-tree/index.md) is a JSON object like this:

``` json
{
	"taxonomy" : [
		{
			"namespace": "cat-geo_en_1.0",
			"categories": [
				{
					"id": "GEO_TAX",
					"label": "Geo Taxonomy",
					"categories": [
						{
							"id": "001.",
							"label": "Afghanistan"
						},
						{
							"id": "002.",
							"label": "Albania"
						},
...
						{
							"id": "193.",
							"label": "Zambia"
						},
						{
							"id": "194.",
							"label": "Zimbabwe"
						}
					]
				}
			]
		}
	]
}
```

`taxonomy` is the root element and it is an array of categories' trees.  
`namespace` is the name of the software module inside the text intelligence engine in which the categories' tree is defined, while `categories` is an array of possibly nested categories.

Each category is an object with these properties:

- `id`: category identifier
- `label`: category label
- `categories`: sub-categories

There can be several categories with the same value for `id` in the categories' tree, but there cannot be two or more categories with the same `id` under the same parent category.

## Templates

The output of the self-documentation resource returning the information extraction [templates](../../../guide/templates/index.md) is a JSON object like this:

``` json
{
	"templates" : [
		{
			"name": "PERSONAL_DATA",
			"fields" : [
				{
					"name" : "FirstName",
					"type" : ""
				},
				{
					"name" : "LastName",
					"type" : ""
				}
			]
		},
		{
			"name": "COMPANY_DATA",
			"fields" : [
				{
					"name" : "Name",
					"type" : "C"
				},
				{
					"name" : "Country",
					"type" : ""
				}
			]
		}            
	]
}
```

 `templates` is the root element and it is an array of template. Each template object has `name` and `fields`.

`name` is the name of a specific template, while `fields` is an array of the fields in the template.

Each field is an object with these properties:

- `name`: field name
- `type`: _C_ is the field was defined as the main field of the template, the empty string otherwise
