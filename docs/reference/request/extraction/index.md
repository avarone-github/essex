# Information extraction request

The [information extraction](../../../guide/extraction/index.md) API request has a JSON object with this format:

``` json
{
	"document": {
		"text": "Your text here."
	},
	"options" : {
		"analysis" : [ "extractions"
	 ],
		"features" : [ "knowledge",
					"dependency", 
					"syncpos"
	 ]
	}
}
```

For the description of the `options`, see the API request [overview](../index.md).

