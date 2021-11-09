# Lemmatization

Lemmatization is the [deep linguistic analysis](../index.md) process that tags [tokens and atoms](../subdivision/index.md) with their corresponding <a href="https://en.wikipedia.org/wiki/Lemma_(morphology)" target="_blank">lemmas</a>.

For example, for this sentence:

	Michael Jordan was one of the best basketball players of all time.

lemmatization produces this output for detected tokens:

Token | Lemma
--- | ---
`Michael Jordan` | `Michael Jordan`
`was` | (to) `be`
`one` | `one`
`of` | `of`
`the` | `the`
`best` | `good`
`basketball players` | `basketball player`
`of` | `of`
`all` | `all`
`time` | `time`
`.` | n/a

In the case of collocations, lemmatization is also applied to constituent atoms.  
For example the token:

	basketball players
	
is a collocation composed of two atoms, for which lemmas are:

	basketball
	player

In the case of <a href="https://en.wikipedia.org/wiki/Anaphora_(linguistics)" target="_blank">anaphoras</a>, the lemma is that of the antecedent or postcedent.  
For example, in the following text:

	Michael Jordan was one of the best basketball players of all time. Scoring was Jordan's stand-out skill, but he still holds a defensive NBA record, with eight steals in a half.
	
lemmatization recognizes _Jordan_ and _he_ in the second sentence as anaphoras, both of which have _Michael Jordan_ as their antecedent in the first sentence, so the returned lemma for the anaphoras will be _Michael Jordan_.

Lemmatization output is part of the [JSON object returned by deep linguistic analysis](../../../reference/output/linguistic-analysis/index.md).