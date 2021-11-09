# Deep linguistic analysis request

The JSON object that constitutes the payload of requests for the [deep linguistic analysis](../../../guide/linguistic-analysis/index.md) API resource must have this structure:

``` json
{
	"document": {
		"text": "Your text here."
	},
	"options" : {
		"analysis" : [ "disambiguation"
	 ],
		"features" : [ "knowledge",
					"dependency", 
					"syncpos"
	 ]
	}
}
```

For the description of the `options`, see the API request [overview](../index.md).

