# Request format

The document analysis, classification and extraction capabilities of the essex API are provided by a POST endpoint.

The request you post must be a JSON object with the following format:

``` json
{
	"document": {
		"text": "Your text here."
	},
	"options" : {
		"analysis" : [ ... ],
		"features" : [ ... ]
	}
}
```

Document text must be encoded with UTF-8.	
The `Content-Type` header of the request must be set to:

	application/json; charset=utf-8

`options` defines the request type. There can be multiple `options` values in a single request.
Here are the possible `analysis` types that can be performed in a single request.

analysis | description
--- | --- 
`disambiguation` | [Deep linguistic analysis](../../guide/linguistic-analysis/index.md), combining a number of linguistic and semantic analyses
`relevants` | [Keyphrase extraction](../../guide/keyphrase-extraction/index.md) extracts the most relevant elements of a text
`entities` | [Named entity recognition](../../guide/entity-recognition/index.md): persons, places, organizations, dates, addresses, etc.
`sentiment` | [Sentiment analysis](../../guide/sentiment-analysis/index.md), how positive or negative the tone of the text is
`relations` | [Relation extraction](../../guide/relation-extraction/index.md) labels concepts in text with their semantic role

The following `features` that can be requested in the output.

features | description
--- | --- 
`knowledge` | Information from the [Knowledge Graph](../../guide/knowledgegraph/index.md) will be returned in the output
`dependency` | Information about the document [Dependency graph](../../reference/dependency-representation/index.md) will be returned in the output
`syncpos` | The returned [positions](../../reference/positions/index.md) are in sync to the original document.

Note:
to be able to safely use the output [positions](../../reference/positions/index.md) on the input text, the `syncpos` feature must be explicitly added to the request, otherwise the exact positioning is not guaranteed.
