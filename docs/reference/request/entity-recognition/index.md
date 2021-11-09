# Named entity recognition request

The [Named entity recognition](../../../guide/entity-recognition/index.md) API request has a JSON object with this format:

``` json
{
	"document": {
		"text": "Your text here."
	},
	"options" : {
		"analysis" : [ "entities"
	 ],
		"features" : [ "knowledge",
					"dependency", 
					"syncpos"
	 ]
	}
}
```

For the description of the `options`, see the API request [overview](../index.md).

