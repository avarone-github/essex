# Sentiment analysis

<a href="https://en.wikipedia.org/wiki/Sentiment_analysis" target="_blank">Sentiment analysis</a> is a type of document analysis that determines how positive or negative the tone of the text is.

Sentiment analysis also performs knowledge linking: [Knowledge Graph](../knowledgegraph/index.md) information and open data&mdash;references to Wikidata, DBpedia, GeoNames, etc.&mdash;are returned for text items that express sentiment given they correspond to syncons of the expert.ai Knowledge Graph. In the case of actual places, geographic coordinates are also provided.

In the reference section of this manual you will find all the information you need to perform sentiment analysis, specifically:

- The [endpoint](../../reference/endpoints/index.md) of the API resource to request.
- The format of the [JSON object](../../reference/request/sentiment-analysis/index.md) which constitutes the payload of the request.
- The format of the [JSON object](../../reference/output/sentiment-analysis/index.md) which constitutes the body of the returned resource.

Here is an example of performing sentiment analysis on a short English text using one of the SDKs available on <a href="https://github.com/therealexpertai/" target="_blank">GitHub</a>:

=== "Python"
    
    The program prints the overall sentiment.

    ``` python
    from expertai.nlapi.edge.client import ExpertAiClient
    client = ExpertAiClient()

    text = "Michael Jordan was one of the best basketball players of all time. Scoring was Jordan's stand-out skill, but he still holds a defensive NBA record, with eight steals in a half." 

    output = client.sentiment(text)

    # Output overall sentiment

    print("Output overall sentiment:")

    print(output.sentiment.overall)
    ```

=== "Java"
    
    The program prints the [JSON response](../../reference/output/entity-recognition/index.md) and the overall sentiment.
    
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

                AnalyzeResponse sentiment = analyzer.sentiment(text);


                // Output JSON representation

                System.out.println("JSON representation:");
                sentiment.prettyPrint();


                // Overall sentiment.

                System.out.println("Overall sentiment:");
                AnalyzeDocument data = sentiment.getData();
                System.out.println(data.getSentiment().getOverall());
            }
            catch(Exception ex) {
                ex.printStackTrace();
            }
        }
    }
    ```

