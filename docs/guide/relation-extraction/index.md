# Relation extraction

Relation extraction is a type of document analysis that labels concepts expressed in the text with their <a href="https://en.wikipedia.org/wiki/Semantic_role_labeling" target="_blank">semantic role</a>.

Relation extraction also performs knowledge linking: [Knowledge Graph](../knowledgegraph/index.md) information and open data&mdash;references to Wikidata, DBpedia, GeoNames, etc.&mdash;are returned for relation items corresponding to syncons of the expert.ai Knowledge Graph. In the case of actual places, geographic coordinates are also provided.

In the reference section of this manual you will find all the information you need to perform relations extraction, specifically:

- The [endpoint](../../reference/endpoints/index.md) of the API resource to request.
- The format of the [JSON object](../../reference/requests/relation-extraction/index.md) to send together with the request.
- The format of the [JSON object](../../reference/output/relation-extraction/index.md) returned.

<!--
Here is an example of performing relation extraction on a short English text using one of the SDKs available on <a href="https://github.com/therealexpertai/" target="_blank">GitHub</a>:

=== "Python"

    The program prints a shallow (no nesting) representation of relations.

    ``` python
    from expertai.nlapi.edge.client import ExpertAiClient
    client = ExpertAiClient()

    text = "Michael Jordan was one of the best basketball players of all time. Scoring was Jordan's stand-out skill, but he still holds a defensive NBA record, with eight steals in a half." 

    output = client.relations(text)

    # Output relations' data

    print("Output relations' data:");

    for relation in output.relations:
        print(relation.verb.lemma, ":");
        for related in relation.related:
            print("\t", "(", related.relation, ")", related.lemma);
    ```

=== "Java"
        
    The program prints a representation of the returned JSON object.
    
    ``` java
    import ai.expert.nlapi.security.Authentication;
    import ai.expert.nlapi.security.Authenticator;
    import ai.expert.nlapi.security.BasicAuthenticator;
    import ai.expert.nlapi.security.DefaultCredentialsProvider;
    import ai.expert.nlapi.v2.API;
    import ai.expert.nlapi.v2.edge.Analyzer;
    import ai.expert.nlapi.v2.edge.AnalyzerConfig;
    import ai.expert.nlapi.v2.message.AnalyzeResponse;

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

                AnalyzeResponse relations = analyzer.relations(text);


                // Output JSON representation

                System.out.println("JSON representation:");
                relations.prettyPrint();
            }
            catch(Exception ex) {
                ex.printStackTrace();
            }
        }
    }
    ```
-->