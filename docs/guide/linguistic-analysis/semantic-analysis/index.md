# Semantic analysis

<a href="https://en.wikipedia.org/wiki/Semantic_analysis_(linguistics)" target="_blank">Semantic analysis</a> is the [deep linguistic analysis](../index.md) process that maps [tokens](../subdivision/index.md) to [Knowledge Graph](../../knowledgegraph/index.md) entries.

This, together with knowledge linking, is what makes linguistic analysys "deep", because it attributes a meaning to each term of the text.

**Note**: tokens corresponding to parts-of-speech like punctuation, conjunctions, articles, prepositions and pronouns are not mapped to Knowledge Graph entries. That isn't because they lack meaning, but because [part-of-speech tagging](../pos-tagging/index.md) and [morphological analysis](../morphological-analysis/index.md) already provide enough information.

Meaning attribution is a relatively easy task if a term is unambiguous.  
The problem arises when a term has <a href="https://en.wikipedia.org/wiki/Polysemy" target="_blank">multiple meanings</a>. For example take the word:

	banks

which can be interpreted as:

- Simple present tense, third person singular of the verb _to bank_ in the sense of "to deposit in a bank"
- Plural form of the noun _bank_ in the sense of "financial institution"
- Plural form of the noun _bank_ in the sense of "slope beside a body of water"

and more. In this case automatic disambiguation is needed, and this is the precisely what semantic analysis does using the [Knowledge Graph](../../knowledgegraph/index.md) and the relationships it contains.

Semantic analysis output is part of the [JSON object returned by deep linguistic analysis](../../../reference/output/linguistic-analysis/index.md).
