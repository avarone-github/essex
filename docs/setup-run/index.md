# Setup and run

## Setup

### Database folder

As mentioned in the [introduction](../index.md), essex exposes the functionalities of text intelligence engines prepared with expert.ai Studio.

When you deploy a project in Studio, you create a **CPK** language package. It is a compressed file with the **.cpk** extension containing all the files that make up the text intelligence engine.

![](studio-deployment.png)

Essex requires that the CPK packages corresponding to the text intelligence engines it must manage are located in a database folder, as exemplified in the following image.

![](database.png)
it is therefore necessary, before being able to run essex, to prepare the database folder in a suitable storage accessible to essex and with enough free space to host all the packages.

!!! info
	In essex jargon, installed CPK packages are referred to as **resources**. However, considering that essex has a RESTful API, the term should not be confused with the vaguely similar concept of <a href="https://www.tutorialspoint.com/restful/restful_resources.htm" target="_blank">REST resources</a>.

To install to and remove CPK packages from the database, follow the instructions below.

### Package installation

To install the CPK package of a text intelligence engine, run this command:

<pre><code><i>executable</i> -dbpath <i>databasefolderpath</i> -install-cpk <i>cpkfilepath</i></code></pre>

where: 

- _`executable`_ is the path of the essex executable file.
- _`databasefolderpath`_ is the path of the database folder.
- `cpkfilepath` is the path of the **.cpk** file

In response to this command, essex creates in the database folder indicated by `databasefolderpath` a subfolder corresponding to the expansion of the **.cpk** file. The subfolder name, also called the **resource name**, is the name of the **.cpk** file without the extension.

The command can be executed regardless of whether essex is already running in single resource or server mode (see below).

### Package removal

To remove a previously installed CPK package you need to ensure that essex if not running in single resource or server mode (see below), then run this command:

<pre><code><i>executable</i> -dbpath <i>databasefolderpath</i> -remove-cpk <i>resourcename</i></code></pre>

where: 

- _`executable`_ is the path of the essex executable file.
- _`databasefolderpath`_ is the path of the database folder.
- `resourcename` is the name of the resource, i.e. the subfolder of `databasefolderpath` in which the CPK package was previously installed.

In response to this command, essex removes the `resourcename` package folder from the the database folder indicated by `databasefolderpath`.

## Run essex

Essex can run in different modes. Depending on the mode, the format of the [request](../reference/requests/index.md) may change.  
Execution mode is determined by the `mode` option which default value is `s`.

### Single resource mode

In single resource mode, essex loads only one text intelligence engine package (CPK) in memory, creating a single running instance of it.

One instance can process only one request at a time, so, when it's busy, all other requests are queued and served on a first-in, first-out basis.

The syntax is:

<pre><code><i>executable</i> -mode -r -dbpath <i>databasefolderpath</i> -resource <i>resourcename</i> [ -hport <i>httpport</i> ] [ -pem <i>pemfile</i> ] [ -ctimeout <i>calltimeout</i> ]</code></pre>

where:

- _`executable`_ is the path of the essex executable file, which is `essex` on Linux and `essex.exe` on Windows.
- _`databasefolderpath`_ is the path of the database folder.
- _`resourcename`_ is the name of the folder, located inside the _`databasefolderpath`_, containing the resource, i.e. the files of the text intelligence engine package to load.
- _`httpport`_ is the TCP port number on which essex listens for HTTP/HTTPS requests for RESTful API resources. The default value is `6090`.
- _`pemfile`_ is the path of a **.pem** file containing SSL private key and certificate. The default value is the empty string, so if the `-pem` option is not specified, essex API uses the HTTP protocol instead of HTTPS.
- `calltimeout` is the timeout, in minutes, before a single call expires. The default value is `10`. A value of `0` means there's no timeout.

### Server mode

In server mode, essex can create multiple in-memory instances of one or more text intelligence engines packages.

At startup you don't specify which packages to load, so essex is essentially "empty" and idle. When a client application specifies the text intelligence engine it requires, essex loads the corresponding package's files and creates an instance of the engine to serve the request.

If an instance of an engine is busy and an analysis request arrives for the same engine, essex tries to fork a new engine instance to handle that request.

The syntax is:

<pre><code><i>executable</i> -mode -s -dbpath <i>databasefolderpath</i> [ -hport <i>httpport</i> ] [ -pem <i>pemfile</i> ] [ -core <i>cores</i>  ] [ -instance <i>instances</i> ] [ -itimeout <i>instancetimeout</i> ] [ -ctimeout <i>calltimeout</i> ]</code></pre>

where:

- _`executable`_ is the path of the essex executable file, which is `essex` on Linux and `essex.exe` on Windows.
- _`databasefolderpath`_ is the path of the database folder.
- _`httpport`_ is the TCP port number on which essex listens for HTTP/HTTPS requests for RESTful API resources. The default value is `6090`.
- _`pemfile`_ is the path of a **.pem** file containing SSL private key and certificate. The default value is the empty string, so if the `-pem` option is not specified, essex API uses the HTTP protocol instead of HTTPS.
- _`core`_ is the maximum number of text intellgence engines instances that can run in parallel.  The default value is number of cores in the machine.
	Once this number is reached, analysis requests for any engine are queued.  
	When an instance becomes free, if it is what is needed to serve the first queued request, it is used, otherwise essex tries to load and instantiate the necessary resource.  
	This parameter is used to limit the number of CPU cores used by essex.
- _`instance`_ is the maximum number of instances loaded in memory. The default value is double the number of cores in the machine.
	A new instance is created in memory, until the value of this parameter is reached, when:
	- essex receives a request for analysis with engine "A" for which no instances exist in memory (it must be loaded from disk).
	- essex receives a request for analysis with engine "B", with one or more instances already in memory, all of which already busy.
	
	This parameter is used to limit the maximum memory used by essex.

- _`itimeout`_ is the maximum time, in hours, that an instance of an engine remains loaded in memory if it is not used. The default value is `1`.
	This parameter is used to recycle memory by freeing up space for other instances. A value of `0` means that instances are never unloaded, even if they are not used.

	!!! warning
		Because of their complexity, some text intelligence engines take a significant amount of time to load, so avoid setting too low values for this parameter.

- `calltimeout` is the timeout, in minutes, before a single call expires. The default value is `10`. Value `0` means no timeout.