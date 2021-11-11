# API Guide

## Capabilities

Essex API capabilities are divided into three groups:

1. [**Document analysis**](full-analysis/index.md), comprising:
	- [Deep linguistic analysis](linguistic-analysis/index.md), which, in turn, comprises:
		- Text subdivision
		- Part-of-speech tagging
		- Morphological analysis
		- Lemmatization
		- Syntactic analysis
		- Semantic analysis
	- [Keyphrase extraction](keyphrase-extraction/index.md)
	- [Named Entity Recognition](entity-recognition/index.md)
	- [Relation extraction](relation-extraction/index.md)
    - [Sentiment analysis](sentiment-analysis/index.md)
2. [**Document classification**](classification/index.md)
3. [**Information extraction**](extraction/index.md)

Document analysis is a standard feature which is available by default in every text intelligence engine produced with <a href="https://docs.expert.ai/studio/latest/" target="_blank">expert.ai Studio</a>.    
Document classification and information extraction, instead, are custom features corresponding to the work of Knowledge Engineers that have instructed the engine to determine what documents are about and to recognize & extract specific text from documents.

The following articles in this section are devoted to describe all the capabilities.

## REST interface

The API has a <a href="https://en.wikipedia.org/wiki/Representational_state_transfer" target="_blank">REST</a> interface that accepts and returns JSON objects.
 
Whenever a client program has to analyze a text, it requests an API **resource** sending the text to analyze, together with parameters, as a JSON payload that's an integral part of the request.  
This is similar to what happens when you you submit a form from a page of Web site using a browser: the submit button sends a request along with a payload constituted by form data.

The request contains the path the resource has inside the API, that is its URL, or _endpoint_.  
The <a href="https://en.wikipedia.org/wiki/POST_(HTTP)" target="_blank">`POST` method</a> is used because it allows to send data, i.e. the JSON object, to the API.

Presented with this request, essex responds synchronously (after an amount of time depending on the type of processing requested, the complexity and the length of the text) by returning the requested resource, that is another JSON object.

In the reference section of this manual you will find all the information about the [endpoints](../reference/endpoints/index.md), the [JSON objects](../reference/requests/index.md) to send with requests and the [JSON objects](../reference/output/index.md) returned by essex.