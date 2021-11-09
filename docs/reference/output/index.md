# API output

## Success

In response to a request for a resource, in case of success, the API returns the HTTP `200 OK` status and a UTF-8 encoded JSON object.

All the [document analysis](../../guide/full-analysis/index.md), [document classification](../../guide/classification/index.md) and [information extraction](../../guide/extraction/index.md) operations share this response format:

<pre>
<code>{
	"success": true,
	"data": {
		"content": <i>analyzedtext</i>,
		"language": <i>languagecode</i>,
		"version": <i>engineinfo</i>,
		<i>resourcespecificproperties</i>
	}
}</code></pre>

Self-documention resources have their [peculiar format](taxonomies-templates/index.md).

The value of the Boolean property `success` indicates that processing was successful while the `data` object contains the results of the analysis.  
The `data` object always has the following properties:

- `content`: the text that's been analyzed.
- `language`: the text language expressed as a <a href="https://en.wikipedia.org/wiki/ISO_639-1" target="_blank">ISO 639-1 language code</a>.
- `version`: text intelligence engine information.

After these properties, resource specific properties (_`resourcespecificproperties`_) follow.  
For more information about those properties, refer to the following articles:

- Document analysis:
	- [Full analysis](full-analysis/index.md)
    - [Deep linguistic analysis](linguistic-analysis/index.md)
	- [Keyphrase extraction](keyphrase-extraction/index.md)
	- [Named entity recognition](entity-recognition/index.md)
	- [Relation extraction](relation-extraction/index.md)
	- [Sentiment analysis](sentiment-analysis/index.md)

- [Document classification](classification/index.md)

- [Information extraction](extraction/index.md)

## Managed errors

In response to a request for a resource, in case of a managed error, the API returns the HTTP `200 OK` status and a UTF-8 encoded JSON object with the following structure:

<pre><code>{
	"success": false
	"errors": [
		{
			"code": <i>errorcode</i>,
			"message": <i>errormessage</i>
		}
	],
}</code></pre>

The value of the Boolean property `success` indicates that processing was not successful while the `error` object contains the error details.

For example, when the request for document analysis or classification resource is a JSON object without the `text` property, you get this object:

``` json
{
	"errors": [
		{
			"code": "PREPARE_DOCUMENT_FAILED",
			"message": "missing layout key in json"
		}
	],
	"success": false
}
```

## Other errors

In case of unmanaged application errors or other anomalies, the API returns specific [HTTP status codes](../http-status-codes/index.md).