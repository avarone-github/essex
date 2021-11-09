# Named entity recognition output

The [named entity recognition](../../../guide/entity-recognition/index.md) resource returns a JSON object with this format:

<pre>
<code>{
	"success": <i>Boolean success flag</i>,
	"data": {
		"content": <i>analyzed text</i>,
		"language": <i>language code</i>,
		"version": <i>technology version info</i>,
		<strong>"knowledge": [],
		"entities": []</strong>
	}
}</code></pre>

For the description of the `contents`, `language` and `version` properties, see the API resources output [overview](../index.md).

## entities

Each item of the `entities` array represents a named entity, for example:

``` json
{
	"lemma": "National Basketball Association",
	"positions": [
		{
			"end": 139,
			"start": 136
		}
	],
	"relevance": 10,
	"syncon": 206693,
	"type": "ORG",
	"attributes": [
		{
			"attribute": "role",
			"lemma": "league",
			"syncon": 36253,
			"type": "org"
		}
	]
}
```

`type` identifies the kind of entity. The possible values for `type` are listed in the [reference section](../../entity-types/index.md).

`positions` is an array containing the [positions](../../positions/index.md) of the entity's mentions in the text.

The `syncon` and the `lemma` properties are the outcome of semantic analysis and lemmatization respectively. These are exactly the same processes carried out during [deep linguistic analysis](../../../guide/linguistic-analysis/index.md). Value -1 for `syncon` means the concept doesn't have a correspondent in the expert.ai [Knowledge Graph](../../../guide/knowledgegraph/index.md). This can happen with entities that are recognized through heuristics (e.g. _John Smith_).

`relevance` is an indicator of the importance of the entity in text. It's values ranges from 1 to 15.

## attributes

The `attributes` array contains information about the entities that is inferred by semantic analysis based on:

- Information available in the [Knowledge Graph](../../../guide/knowledgegraph/index.md)
- Semantic features of the entity's name
- The context in which the entity is cited

The `attribute` property indicates the type of attribute. Possible values are:

Value | Description
--- | ---
`age` | Age of a person
`birthdate` | Birth date of a person
`birthplace` | Birth place of a person
`deathdate` | Death date of a person
`deathplace` | Death date of a person
`gender` | Gender of a person
`humanspec` | Specification of a person
`nationality` | Nationality of a person
`orgspec` | Specification of an organization
`placespec` | Specification of a place
`prodspec` | Specification of a product
`qualifyingadj` | Qualifying adjective
`qualifyingadv` | Qualifying adverb
`qualifyingnoun` | Qualifying noun
`role` | Role of an entity; if referred to a person can also be a title or a profession
`timerangespec` | Interval of time specification
`timespec` | Time specification

<!--
attr
attrspec
attrval
org_placespec 
-->

Attributes can be nested, i.e. an attribute can have other attributes that further specify it.  
For example from the text:

    Saudi King Salman called on governments around the world 

these attributes are inferred for entity _Salman_:

``` json hl_lines="13 14 15 16 17 18 19 20"
"attributes": [
	{
		"attribute": "gender",
		"lemma": "male",
		"syncon": -1,
		"type": ""
	},
	{
		"attribute": "role",
		"lemma": "King",
		"syncon": 43350,
		"type": "nph",
		"attributes": [
			{
				"attribute": "placespec",
				"lemma": "Saudi Arabia",
				"syncon": 38596,
				"type": "GEO"
			}
		],
	}
]
```

The nested attribute, in this case, specifies the place of which entity _Salman_ is the king, as if it were the answer to the question: "king of what?".

For the `syncon` and `lemma` properties see above: they are the result of deep linguistic analysis.

If the attribute is a generic or named entity, `type` identifies the kind of entity. [Possible values](../../entity-types/index.md) can be uppercase or lowercase. Uppercase corresponds to named entities, lowercase to generic entities.

## knowledge

The `knowledge` array contains [Knowledge Graph](../../../guide/knowledgegraph/index.md) data about the syncons associated with the entities. Its contents are described in the article about the output of [full analysis](../full-analysis/index.md#knowledge).