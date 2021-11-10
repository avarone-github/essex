# Document classification

Document classification determines what the document text is about by mapping it to the categories of a [tree](../taxonomies/index.md).

Unlike document analysis, document classification is a custom feature corresponding to the work of Knowledge Engineers that have used <a href="https://docs.expert.ai/studio/latest/" target="_blank">expert.ai Studio</a> to instruct the text intelligence engine.

In the reference section of this manual you will find all the information you need to perform document classification, specifically:

- The [endpoint](../../reference/endpoints/index.md) of the API resource to request.
- The format of the [JSON object](../../reference/request/classification/index.md) to send together with the request.
- The format of the [JSON object](../../reference/output/classification/index.md) returned.

Here is an example of performing document classification on a short English test using one of the SDKs available on <a href="https://github.com/therealexpertai/" target="_blank">GitHub</a>:

=== "Python"
    
     The program prints the list of detected categories.

    ``` python
    from expertai.nlapi.edge.client import ExpertAiClient
    client = ExpertAiClient()

    text = "Michael Jordan was one of the best basketball players of all time. Scoring was Jordan's stand-out skill, but he still holds a defensive NBA record, with eight steals in a half."

    output = client.classification(text)

    print("Tab separated list of categories:")

    for category in output.categories:
        print(category.id_, category.hierarchy, sep="\t")
    ```

=== "Java"
    
    The program prints a representation of the returned JSON object and the list of detected categories.
        
    ``` java
    import ai.expert.nlapi.security.Authentication;
    import ai.expert.nlapi.security.Authenticator;
    import ai.expert.nlapi.security.BasicAuthenticator;
    import ai.expert.nlapi.security.DefaultCredentialsProvider;
    import ai.expert.nlapi.v2.API;
	import ai.expert.nlapi.v2.edge.Analyzer;
	import ai.expert.nlapi.v2.edge.AnalyzerConfig;
    import ai.expert.nlapi.v2.message.AnalyzeResponse;
	import ai.expert.nlapi.v2.model.Category;
	
	import java.util.List;
	
    public class Main {

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

                AnalyzeResponse classification = analyzer.classification(text);


                // Output JSON representation

                classification.prettyPrint();


                // Tab separated list of categories.

                System.out.println("Tab separated list of categories:");
                List<Category> categories = classification.getData().getCategories();

                categories.stream().forEach(c -> System.out.println(c.getId() + "\t" + c.getHierarchy()));
            }
            catch(Exception ex) {
                ex.printStackTrace();
            }
        }
    }
    ```

