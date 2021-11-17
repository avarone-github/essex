# API endpoints

The **endpoints** of the essex API are the addresses&mdash;or URLs&mdash;of its resources.  
Together with the [JSON object](../requests/index.md) that makes up the payload of each request, they identify exactly the resource that the API should return.

The first part of the endpoint, being an URL, is always the protocol, host and port specification, for example:

	https://somehost:6699

This part corresponds to the essex Web service that is listening on the specified TCP port.

The remainder of the endpoint is the resource path and it varies based on the type of functionality required:

- All text analysis resources, whether [document analysis](../../guide/full-analysis/index.md), [document classification](../../guide/classification/index.md) or [information extraction](../../guide/extraction/index.md), share this path:

		/api/analyze

- Self-documentation resources&mdash;[categories' tree](../../guide/categories-tree/index.md), [templates](../../guide/templates/index.md)&mdash;have this path:

		/api/model

<!--
!!! info
	The SDKs available on <a href="https://github.com/therealexpertai/" target="_blank">GitHub</a> automatically take care of building the proper endpoint for each request so you don't have to worry about that detail.
-->