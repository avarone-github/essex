# Morphological analysis

Morphological analysis is the [deep linguistic analysis](../index.md) process that determines lexical and grammatical features of each [token](../subdivision/index.md) in addition to the [part-of-speech](../pos-tagging/index.md).

The result of the analysis is a list of <a href="https://universaldependencies.org/u/feat/index.html" target="_blank">Universal features</a>.

For example, the morphological analysis of the first token of this sentence:

<pre>
<code><span class="bordered">I</span> saw a dandelion on my lawn.
</code></pre>

gives:

	Case=Nom|Number=Sing|Person=1|PronType=Prs

which is a list of feature-value pairs corresponding to:

Pair | Feature label | Feature description | Value label | Value description
--- | --- | --- | --- | ---
`Case=Nom` | `Case` | Case | `Nom` | Nominative
`Number=Sing` | `Number` | Number | `Sing` | Singular
`Person=1` | `Person` | Person | `1` | First
`PronType=Prs` | `PronType` | Pronoun type | `Prs` | Personal

Morphological analysis output is part of the [JSON object returned by deep linguistic analysis](../../../reference/output/linguistic-analysis/index.md).