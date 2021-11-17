# Keyphrase extraction

Keyphrase extraction is a type of document analysis that determines the key elements of a text:

- Relevant topics
- Main sentences
- Main phrases
- Main concepts
- Main lemmas

Main concepts are returned as [Knowledge Graph](../knowledgegraph/index.md) "syncons" and enriched through knowledge linking: open data&mdash;references to Wikidata, DBpedia, GeoNames, etc.&mdash;are returned. In the case of actual places, geographic coordinates are also provided.

Relevant topics are chosen from the Knowledge Graph. You can find a list of relevant topics in the [reference section](../../reference/topics/index.md).

In the reference section of this manual you will find all the information you need to perform keyphrase extraction, specifically:

- The [endpoint](../../reference/endpoints/index.md) of the API resource to request.
- The format of the [JSON object](../../reference/requests/full-analysis/index.md) to send together with the request.
- The format of the [JSON object](../../reference/output/full-analysis/index.md) returned.

<!--
Here is an example of performing keyphrase extraction on an English newspaper article using one of the SDKs available on <a href="https://github.com/therealexpertai/" target="_blank">GitHub</a>:

=== "Python"
       
    In the example, the `document.txt` contains this text:

    ``` text
    At first there was considerable trouble about getting the machine up in the air and the engine well up to speed. They did this by running along a single-rail track perhaps 200 feet long. It was also, in the early experiments, found advisable to run against the wind, because they could then have a greater time to practice in the air and not get so far away from the building where it was stored. Since they can come around to the starting-point, however, they can start with the wind even behind them; and with a strong wind behind it is an easy matter to make even more than a mile a minute. The operator takes his place lying flat on his face. This position offers less resistance to the wind. The engine is started and got up to speed. The machine is held until ready to start by a sort of trap to be sprung when all is ready; then with a tremendous flapping and snapping of the four-cylinder engine, the huge machine springs aloft. When it first turned that circle, and came near the starting-point. I was right in front it; and I said then, and I believe still, it was one of the grandest sights, if not the grandest sight, of my life. Imagine a locomotive that has left its track, and is climbing up in the air right toward you—a locomotive without any wheels, we will say, but with white wings instead, we will further say-a locomotive made of aluminum. Well, now, imagine this white locomotive, with wings that spread 20 feet each way, coming right toward you with a tremendous flap of its propellers, and you will have something like what I saw. The younger brother bade me move to one side for fear it might come down suddenly; but I tell you, friends, the sensation that one feels in such a crisis is something hard to describe. The attendant at one time, when the rope came off that started it, said he was shaking from head to foot as if he had a fit of ague. His shaking was uncalled for, however, for the intrepid manager succeeded in righting up his craft, and she made one of her very best flights. I may add, however, that the apparatus is secured by patents, both in this and in foreign countries; and as nobody else has as yet succeeded in doing any thing like what they have done I hope no millionaire or syndicate will try to rob them of the invention or laurels they have so fairly and honestly earned.  When Columbus discovered America he did not know what the outcome would be, and no one at that time knew; and I doubt if the wildest enthusiast caught a glimpse of what really did come from his discovery. In a like manner these two brothers have probably not even a faint glimpse of what their discovery is going to bring to the children of men. No one living can give a guess of what is coming along this line, much better than any one living could conjecture the final outcome of Columbus' experiment when lie pushed off through the trackless waters. Possibly we may be able to fly over the north pole, even if we should not succeed in tacking the "stars and stripes" to its uppermost end.
    ```
    
    The program prints the list of main lemmas.

    ``` python
    from expertai.nlapi.edge.client import ExpertAiClient
    client = ExpertAiClient()

    file = open("document.txt")
    text = file.read()
    file.close()

    output = client.keyphrase_extraction(text)

    # Main lemmas

    print("Main lemmas:")

    for lemma in output.main_lemmas:
        print(lemma.value)
    ```

=== "Java"

    In the example, the `document.txt` contains this text:

    ``` text
    At first there was considerable trouble about getting the machine up in the air and the engine well up to speed. They did this by running along a single-rail track perhaps 200 feet long. It was also, in the early experiments, found advisable to run against the wind, because they could then have a greater time to practice in the air and not get so far away from the building where it was stored. Since they can come around to the starting-point, however, they can start with the wind even behind them; and with a strong wind behind it is an easy matter to make even more than a mile a minute. The operator takes his place lying flat on his face. This position offers less resistance to the wind. The engine is started and got up to speed. The machine is held until ready to start by a sort of trap to be sprung when all is ready; then with a tremendous flapping and snapping of the four-cylinder engine, the huge machine springs aloft. When it first turned that circle, and came near the starting-point. I was right in front it; and I said then, and I believe still, it was one of the grandest sights, if not the grandest sight, of my life. Imagine a locomotive that has left its track, and is climbing up in the air right toward you—a locomotive without any wheels, we will say, but with white wings instead, we will further say-a locomotive made of aluminum. Well, now, imagine this white locomotive, with wings that spread 20 feet each way, coming right toward you with a tremendous flap of its propellers, and you will have something like what I saw. The younger brother bade me move to one side for fear it might come down suddenly; but I tell you, friends, the sensation that one feels in such a crisis is something hard to describe. The attendant at one time, when the rope came off that started it, said he was shaking from head to foot as if he had a fit of ague. His shaking was uncalled for, however, for the intrepid manager succeeded in righting up his craft, and she made one of her very best flights. I may add, however, that the apparatus is secured by patents, both in this and in foreign countries; and as nobody else has as yet succeeded in doing any thing like what they have done I hope no millionaire or syndicate will try to rob them of the invention or laurels they have so fairly and honestly earned.  When Columbus discovered America he did not know what the outcome would be, and no one at that time knew; and I doubt if the wildest enthusiast caught a glimpse of what really did come from his discovery. In a like manner these two brothers have probably not even a faint glimpse of what their discovery is going to bring to the children of men. No one living can give a guess of what is coming along this line, much better than any one living could conjecture the final outcome of Columbus' experiment when lie pushed off through the trackless waters. Possibly we may be able to fly over the north pole, even if we should not succeed in tacking the "stars and stripes" to its uppermost end.
    ```
    
    The program prints a representation of the returned JSON object and the list of main lemmas.
    
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

    import java.io.IOException;
    import java.nio.file.Files;
    import java.nio.file.Path;
    import java.nio.file.Paths;
    import java.util.stream.Collectors;

    public class Main {

        public static String loadText() {
            try {
                Path path = Paths.get("document.txt");
                return Files.lines(path).collect(Collectors.joining("\r\n"));
            }
            catch(IOException e) {
                return null;
            }
        }

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
                String text = loadText();

                Analyzer analyzer = createAnalyzer();

                AnalyzeResponse relevants = analyzer.relevants(text);


                // Output JSON representation

                System.out.println("JSON representation:");
                relevants.prettyPrint();


                // Main lemmas

                System.out.println("Main lemmas:");
                AnalyzeDocument data = relevants.getData();
                data.getMainLemmas().stream().forEach(c -> System.out.println(c.getValue()));
            }
            catch(Exception ex) {
                ex.printStackTrace();
            }
        }
    }
    ```
-->