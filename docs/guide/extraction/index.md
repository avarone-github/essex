# Information extraction

Information extraction detects meaningful parts of the document by mapping them to [templates](../templates/index.md). It returns **records**&mdash;you can think of a record as an instance of a template&mdash;based on the text matched by extraction rules.

Unlike document analysis, information extraction is a custom feature corresponding to the work of Knowledge Engineers that have used <a href="https://docs.expert.ai/studio/latest/" target="_blank">expert.ai Studio</a> to instruct the text intelligence engine to recognize and extract specific text from documents.

In the reference section of this manual you will find all the information you need to perform information extraction, specifically:

- The [endpoint](../../reference/endpoints/index.md) of the API resource to request.
- The format of the [JSON object](../../reference/request/extraction/index.md) which constitutes the payload of the request.
- The format of the [JSON object](../../reference/output/extraction/index.md) which constitutes the body of the returned resource.

Here is an example of performing information extraction on a short English test using one of the SDKs available on <a href="https://github.com/therealexpertai/" target="_blank">GitHub</a>:

=== "Python"
    
     The program prints the list of records and their fields.

    ``` python
    from expertai.nlapi.edge.client import ExpertAiClient
    client = ExpertAiClient()

    text = "Michael Jordan was one of the best basketball players of all time. Scoring was Jordan's stand-out skill, but he still holds a defensive NBA record, with eight steals in a half."

    output = client.extraction(text)

    print("List of records and their fields:")

    for extraction in output.extractions:
      print(extraction.template)
      for field in extraction.fields:
        print(field.name, field.value, sep="\t")

    ```

=== "Java"
    
    The program prints the [JSON response](../../reference/output/extraction/index.md).
        
    ``` java
    import ai.expert.nlapi.security.Authentication;
    import ai.expert.nlapi.security.Authenticator;
    import ai.expert.nlapi.security.BasicAuthenticator;
    import ai.expert.nlapi.security.DefaultCredentialsProvider;
    import ai.expert.nlapi.v2.API;
    import ai.expert.nlapi.v2.edge.Analyzer;
    import ai.expert.nlapi.v2.edge.AnalyzerConfig;
    import ai.expert.nlapi.v2.message.AnalyzeResponse;
    import ai.expert.nlapi.v2.model.AnalyzeDocument;
	import ai.expert.nlapi.v2.model.Extraction;

    public static Authentication createAuthentication() throws Exception {
            DefaultCredentialsProvider credentialsProvider = new DefaultCredentialsProvider();
            Authenticator authenticator = new BasicAuthenticator(credentialsProvider);
            return new Authentication(authenticator);
        }

        public static Analyzer createAnalyzer() throws Exception {
            return new Analyzer(AnalyzerConfig.builder()
                    .withVersion(API.Versions.V2)
					.withHost(API.DEFAULT_EDGE_HOST)
                    .withAuthentication(createAuthentication())
                    .build());
        }

        public static void main(String[] args) {
            try {
                String text = "Michael Jordan was one of the best basketball players of all time. Scoring was Jordan's stand-out skill, but he still holds a defensive NBA record, with eight steals in a half.";

                Analyzer analyzer = createAnalyzer();

                AnalyzeResponse analysis = analyzer.extraction(text);


                // Output JSON representation

                System.out.println("JSON representation:");
                analysis.prettyPrint();
				
				List<Extraction> extractions = analysis.getData().getExtractions();
            }
            catch(Exception ex) {
                ex.printStackTrace();
            }
        }
    }
    ```

