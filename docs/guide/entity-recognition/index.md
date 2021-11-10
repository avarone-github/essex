# Named entity recognition

<a href="https://en.wikipedia.org/wiki/Named-entity_recognition" target="_blank">Named entity recognition</a> is a type of document analysis.  
It determines which entities&mdash;persons, places, organizations, dates, addresses, etc.&mdash;are mentioned in a text and the attributes of the entity that can be inferred by semantic analysis.

Named entity recognition also performs knowledge linking: [Knowledge Graph](../knowledgegraph/index.md) information and open data&mdash;references to Wikidata, DBpedia, GeoNames, etc.&mdash;are returned for entities corresponding to syncons of the expert.ai Knowledge Graph. In the case of actual places, geographic coordinates are also provided.

Entities are also recognized in pronouns and shorter forms that refer to named mentions.  
This kind of _by reference_ recognition is _anaphoric_ because entities are recognized through <a href="https://en.wikipedia.org/wiki/Anaphora_(linguistics)" target="_blank">anaphoras</a>.
 
For example in this text:

<pre>
<code><span class="bordered">Michael Jordan</span> was one of the best basketball players of all time.
Scoring was <span class="bordered">Jordan</span>'s stand-out skill, but <span class="bordered">he</span> still holds a defensive NBA record, with eight steals in a half.</code></pre>

three mentions of Michael Jordan are recognized:

- the full named mention: _Michael Jordan_
- the anaphoras&mdash;_Jordan_ and _he_&mdash;for which _Michael Jordan_ is considered the antecedent.

In the reference section of this manual you will find all the information you need to perform named entity recognition, specifically:

- The [types](../../reference/entity-types/index.md) of named entities that essex is able to recognize.
- The [endpoint](../../reference/endpoints/index.md) of the API resource to request.
- The format of the [JSON object](../../reference/request/entity-recognition/index.md) to send together with the request.
- The format of the [JSON object](../../reference/output/entity-recognition/index.md) returned.

Here is an example of performing named entity recognition on a short English text using one of the SDKs available on <a href="https://github.com/therealexpertai/" target="_blank">GitHub</a>:

=== "Python"
    
    The program prints the list of entities with their type.

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
        
    The program prints a representation of the returned JSON object and the list of entities with their type.
    
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

                AnalyzeResponse entities = analyzer.entities(text);


                // Output JSON representation

                System.out.println("JSON representation:");
                entities.prettyPrint();


                // Tab separated list of entitites' lemma and type.

                System.out.println("Tab separated list of entities' lemma and type:");
                AnalyzeDocument data = entities.getData();
                data.getEntities().stream().forEach(c -> System.out.println(c.getLemma() + "\t" + c.getType()));
            }
            catch(Exception ex) {
                ex.printStackTrace();
            }
        }
    }
    ```

