# Keyphrase extraction request

The [Keyphrase extraction](../../../guide/keyphrase-extraction/index.md) API request has a JSON object with this format:

``` json
{
	"document": {
		"text": "Your text here."
	},
	"options" : {
		"analysis" : [ "relevants"
	 ],
		"features" : [ "knowledge",
					"dependency", 
					"syncpos"
	 ]
	}
}
```

For the description of the `options`, see the API request [overview](../index.md).

