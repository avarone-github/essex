# Requests

All essex API requests must:

- Use the `POST` method.
- Contain an UTF-8 encoded **JSON object** as their payload.
- Have this header:

		application/json; charset=utf-8

- Be sent to one of the API [endpoints](../endpoints/index.md).

If analysis is required, whether [document analysis](../../guide/full-analysis/index.md), [document classification](../../guide/classification/index.md) or [information extraction](../../guide/extraction/index.md), the JSON object must contain the text to parse.  
In all cases the object contains parameters that specify the request.

For example, the JSON object to send in order to request document classification is like this:

``` json
{
	"document": {
		"text": "Your text here."
	},
	"options": {
		"analysis": [
			"categories"
		],
		"features": [
			"knowledge",
			"dependency",
			"syncpos"
		]
	}
}
```

<!--
!!! info
	The SDKs available on <a href="https://github.com/therealexpertai/" target="_blank">GitHub</a> automatically take care of building the proper JSON object for each request so you don't have to worry about that detail.
-->

[Execution mode](../../setup-run/index.md#run-essex) affects the format of the request. In fact, in server mode, in addition to the text of the document, options and features, it is also necessary to specify the name of the resource that must carry out the analysis. The next articles in this section detail the structure of JSON objects to use to request API resources.

<!--
The `options` property specifies the request type. There can be multiple `options` values in a single request.
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
-->