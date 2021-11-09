# Text subdivision

The text subdivision process is the part of the [deep linguistic analysis](../index.md) that detects text structure in terms of:

- Paragraphs
- Sentences
- Phrases
- Tokens
- Atoms

During this process, the [phrase type](../../../reference/phrase-types/index.md) is also determined.

A **token** can be:

- A <a href="https://en.wikipedia.org/wiki/Collocation" target="_blank">collocation</a>, a sequence of consecutive words recognized as a unit, like _credit card_ or _red carpet_.
- A single word
- A punctuation mark

By definition, an **atom** is something that cannot be further divided. The term is used here to indicate the single words that compose a token.

As an example of text subdivision, consider this text:

	Michael Jordan was one of the best basketball players of all time. Scoring was Jordan's stand-out skill, but he still holds a defensive NBA record, with eight steals in a half.
	Michael Jordan was also a baseball player and an actor.
	
It gets divided in two paragraphs:

	1. Michael Jordan was one of the best basketball players of all time. Scoring was Jordan's stand-out skill, but he still holds a defensive NBA record, with eight steals in a half.
	2. Michael Jordan was also a baseball player and an actor.

The first paragraph is divided in two sentences:

	1. Michael Jordan was one of the best basketball players of all time.
	2. Scoring was Jordan's stand-out skill, but he still holds a defensive NBA record, with eight steals in a half.

The first sentence is divided in six phrases:

	1. Michael Jordan
	2. was
	3. one
	4. of the best basketball players
	5. of all time
	6. .

The fourth phrase is divided into four tokens:

	1. of
	2. the
	3. best
	4. basketball players

Since (in the case of single-word tokens) atoms and tokens coincide, **atoms are returned only for collocations**, so only the fourth token is divided in two atoms:

	1. basketball
	2. player

For each subdivision the process returns:

- Its [position](../../../reference/positions/index.md) in the text
- The reference to the lower level constituent subdivisions

Text subdivision output is part of the [JSON object returned by deep linguistic analysis](../../../reference/output/linguistic-analysis/index.md).