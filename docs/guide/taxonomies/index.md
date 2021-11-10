# Categories' tree

The essex API exposes a self-documentation resource that is the tree of categories detected by [document classification](../classification/index.md).

!!! note
	This resource is useful&mdash;and meaningful&mdash;only if the text intelligence engine has been programmed to perform document classification.

It must be requested using the `POST` method.  
In the reference section of this manual you will find:

- The [endpoint](../../reference/endpoints/index.md) of the API resource to request.
- The format of the [JSON object](../../reference/request/taxonomies-templates/index.md#categories-tree) to send together with the request.
- The format of the [JSON object](../../reference/output/taxonomies-templates/index.md#categories-tree) returned.

Here is an example of getting the categories' tree using one of the SDKs available on <a href="https://github.com/therealexpertai/" target="_blank">GitHub</a>:

=== "Python"
    
    The program prints the list of categories.

    ``` python
    from expertai.nlapi.edge.client import ExpertAiClient

    def printCategory(level, category):
        tabs = "\t" * level
        print(tabs, category.id, "(", category.label, ")")
        for nestedCategory in category.categories:
            printCategory(level + 1, nestedCategory)

    client = ExpertAiClient()

    output = client.taxonomy()

    print("Custom categories' tree:")

    for category in output.taxonomy[0].categories:
        printCategory(1, category)
    ```

=== "Java"
    
    The program fills a `List` variable with categories' information.
    
    ``` java
    import ai.expert.nlapi.security.Authentication;
    import ai.expert.nlapi.security.Authenticator;
    import ai.expert.nlapi.security.BasicAuthenticator;
    import ai.expert.nlapi.security.DefaultCredentialsProvider;
    import ai.expert.nlapi.v2.API;
    import ai.expert.nlapi.v2.edge.Model;
	import ai.expert.nlapi.v2.edge.ModelConfig;
    import ai.expert.nlapi.v2.message.TaxonomyModelResponse;
	import ai.expert.nlapi.v2.model.Taxonomy;
	
	import java.util.List;

    public class Main {

        public static Model createModel() throws Exception {
			return new Model(ModelConfig.builder()
                         .withVersion(API.Versions.V2)
                         .withHost(API.DEFAULT_EDGE_HOST)
                         .build());
		}

        public static void main(String[] args) {
            try {
                Model model = createModel();
            
				TaxonomyModelResponse taxModelResponse = model.taxonomy();
				List<Taxonomy> taxonomies = taxModelResponse.getData();
            }
            catch(Exception ex) {
                ex.printStackTrace();
            }
        }
    }
    ```
