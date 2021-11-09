# Part-of-speech tagging

## Standard tagging

Standard <a href="https://en.wikipedia.org/wiki/Part-of-speech_tagging" target="_blank">part-of-speech tagging</a> is the [deep linguistic analysis](../index.md) process that marks up each [token](../subdivision/index.md) with the corresponding <a href="https://universaldependencies.org/u/pos/" target="_blank">Universal POS tag</a>.

For example, for this sentence:

	Michael Jordan was one of the best basketball players of all time.

standard part-of-speech tagging produces this output:

Token | Part-of-speech | Universal POS tag
--- | --- | ---
`Michael Jordan` | Proper noun | `PROPN`
`was` | Auxiliary | `AUX`
`one` | Numeral | `NUM`
`of` | Adposition | `ADP`
`the` | Determiner | `DET`
`best` | Adjective | `ADJ`
`basketball players` | Noun | `NOUN`
`of` | Adposition | `ADP`
`all` | Determiner | `DET`
`time` | Noun | `NOUN`
`.` | Punctuation | `PUNCT`

Standard part-of-speech tagging output is part of the [JSON object returned by deep linguistic analysis](../../../reference/output/linguistic-analysis/index.md).

## Custom tagging

In addition to standard part-of-speech tagging, [deep linguistic analysis](../index.md) marks up both [tokens and atoms](../subdivision/index.md) with custom expert.ai [type labels](../../../reference/expert-ai-types).  
expert.ai types combine part-of-speech information with entity type information.  
For example, for the following sentence:

	Please Travis, take me to Avalon. Do you mind if I bring my dog Bella with me?
	
custom tagging is:

Token | Type description | Custom expert.ai label
--- | --- | ---
`Please` | Adverb | `ADV`
`Travis` | Proper name of a human being | `NPR.NPH`
`,` | Punctuation | `PNT`
`take` | Verb | `VER`
`me` | Pronoun | `PRO`
`to` | Preposition | `PRE`
`Avalon` | Proper noun of an extra-terrestrial or imaginary place | `GEX`
`.` | Punctuation | `PNT`
`Do` | Auxiliary verb | `AUX`
`you` | Pronoun | `PRO`
`mind` | Verb | `VER`
`if` | Conjunction | `CON`
`I` | Pronoun | `PRO`
`bring` | Verb | `VER`
`my` | Adjective | `ADJ`
`dog` | Noun | `NOU`
`Bella` | Proper noun of an animal | `NPR.ANM`
`with` | Preposition | `PRE`
`me` | Pronoun | `PRO`
`?` | Punctuation | `PNT`

As mentioned above, the expert.ai type is also attributed to atoms, while standard part-of-speech tagging stops at the token level.

Custom part-of-speech tagging output is part of the [JSON object returned by deep linguistic analysis](../../../reference/output/linguistic-analysis/index.md).