# The Knowledge Graph

The expert.ai Knowledge Graph is a concept-based representation of universal or domain-specific knowledge for a given language.

Each entry in the Knowledge Graph corresponds to a concept.

There are entries for common nouns, proper nouns, verbs, adjectives and adverbs.

<!--Other parts of speech like punctuation, conjunctions, articles, prepositions and pronouns are not modeled in the Knowledge Graph because the text analysis software has its own ability to recognize these parts.-->

<!--Ideally, the Knowledge Graph should have an entry for each of the concepts that can be expressed in the given language. This is practically feasible only in the case of relatively little or consolidated knowledge domains. However, the coverage of universal Knowledge Graphs is vast and expert.ai constantly takes care of keeping them updated.-->

Each entry contains information, for example:

- The terms that can be used to express the concept in a text, for example _hand, pass, pass on, hand off, turn over, reach_.
- the corresponding part-of-speech&mdash;for example _(to) climb_ &rarr; verb&mdash;and other grammatical information on the terms.
- The topics to which the concept corresponds, for example _soprano_ &rarr; opera, singing.
- References to external knowledge bases such as Wikidata, DBpedia, GeoNames, etc.
- Extended proprieties, for example the coordinates of places.

Modeling concepts that can be expressed in a language are not sufficient to enable the text analysis software to interpret ambiguous terms alone.

For example, consider that in the expert.ai universal Knowledge Graph for the English language there are more than 20 entries for the verb _(to) put_.  
The single entry has statistical information indicating the frequency with which the concept is used in a reference corpus compared to other concepts that can be expressed with the same word. This information is useful for disambiguation, but insufficient. Using statistics alone can lead to incorrect interpretations and to a textual analysis of low quality and even lower usefulness.

What really improves the results are the _relationships_ between concepts, hence the term Knowledge _Graph_. A single entry is linked to one or more other entries and, as such, relationships can be numerous.  
For example, a concept can be connected to other concepts in the hierarchical relationship called "IS-A". So:

	sodium
	IS A
	alkaline metal
	IS A
	metal
	IS A
	element

Or there can be a "part-whole" relationship:

	wheel
	IS A PART OF
	car

	clutch
	IS A PART OF
	car

	dashboard
	IS A PART OF
	car

Relationships are designed to be navigated in both directions, so from the concept of _car_ it is possible to discover the parts that make it up (wheels, clutch, dashboard, etc.) by navigating the "IS PART OF" relationships downstream. In the same way, for the "IS-A" relationship, starting from the concept of _alkaline metal_ it is possible to discover which elements are "types of" the parent concept (sodium, cesium, lithium, etc.).

Relationships can be one-to-many. If this is obvious for the "part-whole" relations if read from the "whole" to the parts and for the "IS A" relationship if read from the more generic concept to the more specific ones, it is not obvious in the opposite direction. However it can be, for example:

	cat
	IS A
	feline

but also:

	cat
	IS A
	pet

So it is possible that in a hierarchical relationship a concept can have multiple "parents".

The relationships between Knowledge Graph entries are the foundations of solid disambiguation.  
Suppose the text contains a form of the verb _(to)_ _put_. As stated, the standard English Knowledge Graph contains more than 20 different concepts that can be expressed with _(to)_ _put_, but which is the right one?

Relationships can help. The text analysis software can explore the relationships of each concept to find out if the concept itself is linked to other concepts expressed in the same text.
The concept with more links to other concepts is a good candidate for the "right concept".

The disambiguation of one word helps to disambiguate the others, but the text analysis software is always free to "go back" and correct its previous clarification choices as it proceeds with the analysis of the other words of the text, with a chain effect on other disambiguations.

The name used by expert.ai to designate an entry in a Knowledge Graph is _syncon_.