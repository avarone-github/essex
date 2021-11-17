# Templates

A template is the set of fields that [information extraction](../extraction/index.md) can fill with data to create records. The essex API provides a self-documentation resource returning all the defined templates.

!!! note
	This resource is useful&mdash;and meaningful&mdash;only if the text intelligence engine has been programmed to perform information extraction.

It must be requested using the `POST` method.  
In the reference section of this manual you will find:

- The [endpoint](../../reference/endpoints/index.md) of the API resource to request.
- The format of the [JSON object](../../reference/requests/taxonomies-templates/index.md#templates) to send together with the request.
- The format of the [JSON object](../../reference/output/taxonomies-templates/index.md#templates) returned.

<!--
Here is an example of getting the templates using one of the SDKs available on <a href="https://github.com/therealexpertai/" target="_blank">GitHub</a>:

=== "Python"
    
    The program prints the list of templates along with their fields.

    ``` python
    from expertai.nlapi.edge.client import ExpertAiClient

    client = ExpertAiClient()

    output = client.templates()

    print("Templates:")

    for template in output.templates:
      print(template.name)
      for field in template.fields:
        print(field.name)
    ```

=== "Java"
    
    The program fills a `List` variable with templates' information.
    
    ``` java
    import ai.expert.nlapi.security.Authentication;
    import ai.expert.nlapi.security.Authenticator;
    import ai.expert.nlapi.security.BasicAuthenticator;
    import ai.expert.nlapi.security.DefaultCredentialsProvider;
    import ai.expert.nlapi.v2.API;
    import ai.expert.nlapi.v2.edge.Model;
	import ai.expert.nlapi.v2.edge.ModelConfig;
    import ai.expert.nlapi.v2.message.TemplatesModelResponse;
	import ai.expert.nlapi.v2.model.TemplateNamespace;
	
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
            
				TemplatesModelResponse templModelResponse = model.templates();
				List<TemplateNamespace> templates = templModelResponse.getData();
            }
            catch(Exception ex) {
                ex.printStackTrace();
            }
        }
    }
    ```
-->