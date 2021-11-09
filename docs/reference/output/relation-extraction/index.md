# Relation extraction output

The [relation extraction](../../../guide/relation-extraction/index.md) resource returns a JSON object with this format:

<pre>
<code>{
	"success": <i>Boolean success flag</i>,
	"data": {
		"content": <i>analyzed text</i>,
		"language": <i>language code</i>,
		"version": <i>technology version info</i>,
		<strong>"paragraphs": [],
		"sentences": [],
		"phrases": [],
		"tokens": [],
        "knowledge": [],
		"relations": []</strong>
	}
}</code></pre>

For the description of the `contents`, `language` and `version` properties, see the API resources output [overview](../index.md).

The `paragraphs`, `sentences`, `phrases` and `tokens` arrays are produced by the [text subdivision process](../../../guide/linguistic-analysis/subdivision/index.md). These sections are described in the article about the [output of the deep linguistic analysis](../linguistic-analysis/index.md).

The `knowledge` array contains [Knowledge Graph](../../../guide/knowledgegraph/index.md) data about the relations elements, as a result of the [semantic analysis](../../../guide/linguistic-analysis/semantic-analysis/index.md) process. Its contents are described in the article about the output of [full analysis](../full-analysis/index.md#knowledge).

## relations

Each item of the `relations` array represents a verb plus the text elements that are in a semantic relation with it. These elements may specify arguments, adjuncts or subordinate clauses.
For example, given this input text:

    John sent a letter to Mary.
    
the `relations` array can contain an item like this:

``` json
{
	"verb": {
		"text": "sent",
		"lemma": "send",
		"syncon": 68296,
		"phrase": 1,
		"type": "",
		"relevance": 15
	},
	"related": [
		{
			"relation": "sbj_who",
			"text": "John",
			"lemma": "John",
			"syncon": -1,
			"type": "NPH",
			"phrase": 0,
			"relevance": 15
		},
		{
			"relation": "obj_what",
			"text": "a letter",
			"lemma": "letter",
			"syncon": 29131,
			"type": "wrk",
			"phrase": 2,
			"relevance": 10
		},
		{
			"relation": "to_who",
			"text": "to Mary",
			"lemma": "Mary",
			"syncon": -1,
			"type": "NPH",
			"phrase": 3,
			"relevance": 10
		}
	]
}
```

### Common properties

The `verb` object and the items of the `related` array share some properties.

`text` if the portion of text corresponding to the element.

`phrase` is the index of the phrase containing the element. The value must be interpreted as a pointer to an item of the `phrases` array, where the positions of the first and the last character of the phrase can be found. This information can be used for text highlighting.  
From the phrase it is possible to go back to the sentence it belongs to&mdash;using the `sentences` array&mdash;and from the sentence to the paragraph&mdash;using the `paragraphs` array&mdash;,or, going in the opposite direction, to find the tokens contained in the phrase &mdash;using the `tokens` array.  
Subordinate clauses&mdash;related items having the `relation` property set to `sub`&mdash;do not have a one-to-one correspondence with a phrase. In that case, `phrase` has the conventional value -1.

The `syncon` and `lemma` properties are the outcome of semantic analysis and lemmatization respectively. These are exactly the same processes carried out during [deep linguistic analysis](../../../guide/linguistic-analysis/index.md). Value -1 for `syncon` means the concept doesn't have a correspondent in the expert.ai [Knowledge Graph](../../../guide/knowledgegraph/index.md). This can happen with:

1. entities having a proper noun that are recognized through heuristics (e.g. _John Smith_)
2. parts-of-speech that ar not mapped in the Knowledge Graph like pronouns (e.g., _them_)
3. subordinate clauses like quotes (e.g., _John said: "**I will do it!**"_)

In cases 1 and 2 `lemma` is an empty string.

`relevance` is an indicator of the importance of the element in text. Its values ranges from 1 to 15. When element importance cannot be determined, `relevance` has the conventional value -1.

### verb

The `verb` object is always present and it represents the verb.  
  
`type` is the verb type. When set, it can be one of the following:

Verb type | Description
--- | ---
`CPL` | _to be_ used as a connection as in _John **is** a smart guy_
`MOV` | Verb of movement like _to go_
`SAY` | Verb of communication like _to say_

### related

The items of the `related` array represent text elements that are related to the verb.
 
`relation` is the type of relation and can be one of the following:
 
Possible values of `relation` |
--- |
`sbj_who` |
`sbj_what` |
`obj_who` |
`obj_what` |
`is_who` |
`is_what` |
`to_who` |
`to_what` |
`using_what` |
preposition* + `_what` |
preposition* + `_who` |
`sub`** |
`when` |
`where` |
`to_where` |
`from_where` |
`in_where` |
`which_way` |
`how` |
`of_age` |
`limited_to` |

\* Prepositions are expressed in the language specified for the analysis, so, for example, a possible value in the case of German language could be `auf_what`. Multi-word prepositional expressions like _according to_, _in front of_, ecc., are written in compact form (`accordingto`, `infrontof`).

\*\* The `sub` relation type is used for subordinate clauses.

`type` identifies the kind of element. [Possible values](../../entity-types/index.md) can be uppercase or lowercase. Uppercase corresponds to named entities, lowercase to generic entities.

Relations can be recursive: a related item can be related to another item and so on. In this case an item of the `related` array can contain a `related` array.  
For example, given this input text:

    Mireille placed the plant pot on the landing at the top of the stairs.
    
relations can be like this:

``` json hl_lines="34 35 36 37 38 39 40 41 42 43 44"
"relations": [
	{
		"related": [
			{
				"lemma": "Mireille",
				"phrase": 0,
				"relation": "sbj_who",
				"relevance": 14,
				"syncon": -1,
				"text": "Mireille",
				"type": "NPH"
			},
			{
				"lemma": "pot",
				"phrase": 2,
				"relation": "obj_what",
				"relevance": 15,
				"syncon": 18506,
				"text": "the plant pot",
				"type": "prd"
			},
			{
				"lemma": "landing",
				"phrase": 3,
				"relation": "on_what",
				"relevance": 5,
				"syncon": 16859,
				"text": "on the landing",
				"type": "bld"
			},
			{
				"lemma": "top",
				"phrase": 4,
				"related": [
					{
						"lemma": "stairs",
						"phrase": 5,
						"relation": "of_what",
						"relevance": 1,
						"syncon": 20016,
						"text": "of the stairs",
						"type": "bld"
					}
				],
				"relation": "at_what",
				"relevance": -1,
				"syncon": 37732,
				"text": "at the top",
				"type": ""
			}
		],
		"verb": {
			"lemma": "place",
			"phrase": 1,
			"relevance": 15,
			"syncon": 68498,
			"text": "placed",
			"type": ""
		}
	}
]
```

## knowledge

The `knowledge` array contains [Knowledge Graph](../../../guide/knowledgegraph/index.md) data for the items of the `relations` array. Its contents are described in the article about the output of [full analysis](../full-analysis/index.md#knowledge).