# Execution modes

## Resource mode

In resource mode, essex loads one text intelligence engine and spins up a single instance of it.  
One instance can process only one request at a time, so when it's busy all other requests are queued.

The syntax is:

<pre><code><i>executable</i> -mode -r -dbpath <i>enginesfolder</i> -module cogito -resource <i>enginefoldername</i> -hport <i>portnumber</i> [ -pem <i>pemfile</i> ]</code></pre>

where:

- _`executable`_ is the path to the essex executable file.
- _`enginesfolder`_ is the path to the folder containing the text intelligence engine folders.
- _`enginefoldername`_ is the name of the folder, located inside the _`enginesfolder`_ folder, containing the files of the text intelligence engine to load.
- _`portnumber`_ is the TCP port number on which essex listens for requests for RESTful API resources.
- _`pemfile`_ is the path of a **.pem** file containing SSL private key and certificate. If the `-pem` option is specified, essex API uses the HTTPS protocol instead of HTTP.

## Server mode

In server mode, essex can load in memory more instances of text intelligence engines, running multiple instances of those engines in parallel.  
At startup you don't specify which text intelligence engines to load so essex is essentially "empty" and idle. When a client application specifies the text intelligence engine it requires, essex automatically loads the engine's files from disk to memory and creates an instance of the engine to serve the request.  
If an instance of an engine is busy and an analysis request arrives for the same engine, essex tries to fork a new engine instance to handle that request.

The syntax is:

<pre><code><i>executable</i> -mode -s -dbpath <i>enginesfolder</i> -module cogito -hport <i>portnumber</i> [ -pem <i>pemfile</i> ] -core <i>cores</i> -instance <i>instances</i> -itimeout <i>instancetimeout</i></code></pre>

where:

- _`executable`_ is the path to the essex executable file.
- _`enginesfolder`_ is the path to the folder containing the text intelligence engine folders.
- _`portnumber`_ is the TCP port number on which essex listens for requests for RESTful API resources.
- _`pemfile`_ is the path of a **.pem** file containing SSL private key and certificate. If the `-pem` option is specified, the essex API uses the HTTPS protocol instead of HTTP.
- _`core`_ is the maximum number of text intellgence engine instances that can run in parallel.  
	Once this number is reached, any analysis requests for any engine are queued.  
	When an instance becomes free, if it is what is needed to serve the queued request, it is used, otherwise it is shut down&mdash;but kept in memory&mdash;and the necessary resource is started in its place.  
	This parameter is used to limit the number of CPU cores used by essex.
- _`instance`_ is the maximum number of instances loaded in memory. A new instance is created in memory, until the value of this parameter is reached, when:
	- essex receives a request for analysis with engine "X" for which no instances exist in memory (it must be loaded from disk).
	- essex receives a request for analysis with engine "Y", with one or more instances already in memory, all of which already busy.
	
	This parameter is used to limit the maximum memory used by essex.

- _`itimeout`_ is the maximum time that an instance of an engine remains loaded in memory if it is not used. This parameter is used to recycle memory by freeing up space for other instances. A value of 0 means that instances are never unloaded, even if they are not used.

	!!! warning
		Because of their complexity, some text intelligence engines take a significant amount of time to load, so avoid setting too low values for this parameter.