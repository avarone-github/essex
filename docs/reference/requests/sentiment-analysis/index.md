# Sentiment analysis requests

The JSON object that constitutes the payload of requests for [sentiment analysis](../../../guide/sentiment-analysis/index.md) must be like this:

``` json
{
	"document": {
		"text": "Your text here."
	},
	"options": {
		"analysis": [
			"sentiment"
		],
		"features": [
			"knowledge",
			"dependency",
			"syncpos"
		]
	}
}
```