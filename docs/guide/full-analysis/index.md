# Full analysis

Full document analysis is the sum of:

- [Deep linguistic analysis](../linguistic-analysis/index.md)
- [Keyphrase extraction](../keyphrase-extraction/index.md)
- [Named entity recognition](../entity-recognition/index.md).  
- [Relation extraction](../relation-extraction/index.md)
- [Sentiment analysis](../sentiment-analysis/index.md)

Document analysis is a standard feature which is available by default in every text intelligence engine produced with <a href="https://docs.expert.ai/studio/latest/" target="_blank">expert.ai Studio</a> (no coding required). 

In the reference section of this manual you will find all the information you need to perform full document analysis, specifically:

- The [endpoint](../../reference/endpoints/index.md) of the API resource to request.
- The format of the [JSON object](../../reference/requests/full-analysis/index.md) to send together with the request.
- The format of the [JSON object](../../reference/output/full-analysis/index.md) returned.

<!--
Here is an example of performing full document analysis on a short English text using one of the SDKs available on <a href="https://github.com/therealexpertai/" target="_blank">GitHub</a>:

=== "Python"
    
    The program prints the number of items for each of the output's arrays.

    ``` python
    from expertai.nlapi.edge.client import ExpertAiClient
    client = ExpertAiClient()

    text = "Michael Jordan was one of the best basketball players of all time. Scoring was Jordan's stand-out skill, but he still holds a defensive NBA record, with eight steals in a half.'" 
    
    output = client.full_analysis(text)

    # Output arrays size

    print("Output arrays size:");

    print("knowledge: ", len(output.knowledge))
    print("paragraphs: ", len(output.paragraphs))
    print("sentences: ", len(output.sentences))
    print("phrases: ", len(output.phrases))
    print("tokens: ", len(output.tokens))
    print("mainSentences: ", len(output.main_sentences))
    print("mainPhrases: ", len(output.main_phrases))
    print("mainLemmas: ", len(output.main_lemmas))
    print("mainSyncons: ", len(output.main_syncons))
    print("topics: ", len(output.topics))
    print("entities: ", len(output.entities))
    print("relations: ", len(output.relations))
    print("sentiment.items: ", len(output.sentiment.items))
    ```

=== "Java"
    
    The program prints the number of items for each of the output's arrays.
        
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

                AnalyzeResponse analysis = analyzer.analyze(text);


                // Output JSON representation

                System.out.println("JSON representation:");
                analysis.prettyPrint();


                // Output arrays size

                System.out.println("Output arrays size:");
                AnalyzeDocument data = analysis.getData();

                System.out.println("knowledge: " + data.getKnowledge().size());
                System.out.println("paragraphs: " + data.getParagraphs().size());
                System.out.println("sentences: " + data.getSentences().size());
                System.out.println("phrases: " + data.getPhrases().size());
                System.out.println("tokens: " + data.getTokens().size());
                System.out.println("mainSentences: " + data.getMainSentences().size());
                System.out.println("mainPhrases: " + data.getMainPhrases().size());
                System.out.println("mainLemmas: " + data.getMainLemmas().size());
                System.out.println("mainSyncons: " + data.getMainSyncons().size());
                System.out.println("topics: " + data.getTopics().size());
                System.out.println("entities: " + data.getEntities().size());
                System.out.println("relations: " + data.getRelations().size());
                System.out.println("sentiment/items: " + data.getSentiment().getItems().size());
            }
            catch(Exception ex) {
                ex.printStackTrace();
            }
        }
    }
    ```
-->