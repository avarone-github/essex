# Deep linguistic analysis overview

Deep linguistic analysis is a type of document analysis that combines the following interdependent processes:

- [Text subdivision](subdivision/index.md)
- [Part-of-speech tagging](pos-tagging/index.md)
- [Morphological analysis](morphological-analysis/index.md)
- [Lemmatization](lemmatization/index.md)
- [Syntactic analysis](syntactic-analysis/index.md)
- [Semantic analysis](semantic-analysis/index.md)

The analysis is "deep" because, together with common linguistic analysis, it also:

- Disambiguates the terms of the text, i.e. picks one of all the possible meanings.
- Performs knowledge linking: [Knowledge Graph](../knowledgegraph/index.md) information and open data&mdash;references to Wikidata, DBpedia, GeoNames , etc.&mdash;are returned for text tokens corresponding to concepts of the expert.ai Knowledge Graph.

	!!! info
		In the case of actual places, geographic coordinates are also provided.

In the manual's reference section you will find all the information required to perform deep linguistic analysis, specifically:

- The [endpoint](../../reference/endpoints/index.md) of the API resource to request.
- The format of the [JSON object](../../reference/requests/linguistic-analysis/index.md) to send together with the request.
- The format of the [JSON object](../../reference/output/linguistic-analysis/index.md) returned.

Here is an example of performing deep linguistic analysis on a short English text using one of the SDKs available on <a href="https://github.com/therealexpertai/" target="_blank">GitHub</a>:

=== "Python"

    The program prints a the list of tokens' lemmas with their part-of-speech.

    ``` python
    from expertai.nlapi.edge.client import ExpertAiClient
    client = ExpertAiClient()

    text = "Michael Jordan was one of the best basketball players of all time. Scoring was Jordan's stand-out skill, but he still holds a defensive NBA record, with eight steals in a half." 

    output = client.deep_linguistic_analysis(text)

    # Output tokens' data

    print("Output tokens' data:");

    print (f'{"TEXT":{20}} {"LEMMA":{40}} {"POS":{6}}')
    print (f'{"----":{20}} {"-----":{40}} {"---":{6}}')

    for token in output.tokens:
        print (f'{text[token.start:token.end]:{20}} {token.lemma:{40}} {token.pos:{6}}')
    ```

=== "Java"
    
    The program prints a representation of the returned JSON object and a list of tokens' lemmas with their part-of-speech.
    
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

                AnalyzeResponse disambiguation = analyzer.disambiguation(text);


                // Output JSON representation

                System.out.println("JSON representation:");
                disambiguation.prettyPrint();


                // Tokens' lemma and part-of-speech

                System.out.println("Tab separated list of tokens' lemma and part-of-speech:");
                AnalyzeDocument data = disambiguation.getData();
                data.getTokens().stream().forEach(c -> System.out.println(c.getLemma() + "\t" + c.getPos()));
            }
            catch(Exception ex) {
                ex.printStackTrace();
            }
        }
    }
    ```

