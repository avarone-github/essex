# 3. Make your first call

Once you have the [client](../setup-client-tools/index.md) and the [server](../setup-server/index.md) set up, you can try out [named entity recognition](../../guide/entity-recognition/index.md) on a short English text.

=== "Python"
    
    In order to use the API you must have an expert.ai developer account. Visit the [developer portal](https://developer.expert.ai/) and sign up to get one.
    
    The Python client needs to know your account credentials. It can get them from two environment variables:
    
    ``` text
    EAI_USERNAME
    EAI_PASSWORD
    ```
       
    Set those variables before running the script below.
    
    The script prints out the named entities recognized in a short English text.

    ``` python
    from expertai.nlapi.edge.client import ExpertAiClient
    client = ExpertAiClient()

    text = "Michael Jordan was one of the best basketball players of all time. Scoring was Jordan's stand-out skill, but he still holds a defensive NBA record, with eight steals in a half."

    output = client.named_entity_recognition(text)

    print (f'{"ENTITY":{50}} {"TYPE":{10}}')
    print (f'{"------":{50}} {"----":{10}}')

    for entity in output.entities:
        print (f'{entity.lemma:{50}} {entity.type_:{10}}')
    ```

=== "Java"
    
    In order to use the API you must have an expert.ai developer account. Visit the [developer portal](https://developer.expert.ai/) and sign up to get one.
    
    The Java client needs to know your account credentials. It can get them from two environment variables:
    
    ``` text
    EAI_USERNAME
    EAI_PASSWORD
    ```
    
    Set those variables with you account credentials before running the sample program below.
        
    The program prints a JSON object containing the entities recognized in a short English text.
    
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
                String text = "Michael Jordan was one of the best basketball players of all time. Scoring was Jordan's stand-out skill, but " +
                              "he still holds a defensive NBA record, with eight steals in a half.";

                Analyzer analyzer = createAnalyzer();

                AnalyzeResponse entities = analyzer.entities(text);


                // Output JSON representation

                entities.prettyPrint();
            }
            catch(Exception ex) {
                ex.printStackTrace();
            }
        }
    }
    ```

## The next step

Now that you took a first look at the Edge API, discover its [capabilites](../../guide/index.md) and learn more about [using it](../../how-to/index.md).