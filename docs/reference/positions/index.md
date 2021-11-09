# Positions

Analysis, classification and extraction return positions. For example:

- The deep linguistic analysis resource returns the positions of all the subdivisions of the text (paragraphs, sentences, phrases, tokens and atoms).
- The keyphrase extraction resource returns the positions of main sentences, main phrases, main concepts and main lemmas.
- The classification resources return the positions of the parts of the text help identify a
certain category.

All these positions refer to the analyzed text, that is the `content` property of the `data` object.

Note: To force the positions to be in sync with the original text sent in the request, even when it is transformed by the engine, the `feature` with name `syncpos` must be added to the request, as specified in the [request general format description](../../reference/request/index.md).



The starting position is returned in the `start` property and the ending position in the `end` property.

The value of the `start` property is the zero-based index of the first character of the block.  
For example, if a text begins with:

	Michael Jordan was one of the best basketball players of all time.

the start position of phrase _of all time_ is 54:

<pre>
<code>
Michael Jordan was one of the best basketball players <span class="bordered">of all time</span>.
                                                      &uarr;
012345678901234567890123456789012345678901234567890123<strong>4</strong>5678901234567890
0         1         2         3         4         <strong>5</strong>         6         7
</code>
</pre>
	
The value of the `end` position is the zero-based index of the first character after the text block.
In the example case above, the end position of the phrase is 65:

<pre>
<code>
Michael Jordan was one of the best basketball players <span class="bordered">of all time</span>.
                                                                 &uarr;
01234567890123456789012345678901234567890123456789012345678901234<strong>5</strong>67890
0         1         2         3         4         5         <strong>6</strong>         7
</code>
</pre>
