# Dependency Parsing

For dependency parser, the [English EWT](https://github.com/UniversalDependencies/UD_English-EWT) universal dependency dataset is used.
The corpus comprises 254,825 words and 16,621 sentences, taken from five genres of web media: weblogs, newsgroups,
emails, reviews, and Yahoo! answers. The trees were automatically converted into Stanford Dependencies and then hand-corrected to Universal Dependencies

The following are the evaluation metrics for the Udpipe parser for this corpus:

```text
Metrics    | Precision |    Recall |  F1 Score | AligndAcc
-----------+-----------+-----------+-----------+-----------
Tokens     |    100.00 |    100.00 |    100.00 |
Sentences  |    100.00 |    100.00 |    100.00 |
Words      |    100.00 |    100.00 |    100.00 |
UPOS       |    100.00 |    100.00 |    100.00 |    100.00
XPOS       |    100.00 |    100.00 |    100.00 |    100.00
Feats      |    100.00 |    100.00 |    100.00 |    100.00
AllTags    |    100.00 |    100.00 |    100.00 |    100.00
Lemmas     |    100.00 |    100.00 |    100.00 |    100.00
UAS        |     85.47 |     85.47 |     85.47 |     85.47
LAS        |     83.45 |     83.45 |     83.45 |     83.45
```

Based on the metrics listed above, the Udpipe parser performs well, with LAS and UAS F1 scores of `83.45` and `85.47`, respectively.

When looking at the first 20-30 lines of output. The majority of the sentences were correctly parsed, but in some cases,
the Part of Speech tagger was incorrect, resulting in an error in the dependency parsing output.

Here are couple of examples:

* For the sentence `One of the pictures shows a flag that was found in Fallujah`.
  * The word `that` should be `determiner` where as in the output it is marked as `pronoun`.
* For the sentence `Compare the flags to the Fallujah one.`
  * The word `Fallujah` should be `noun` but it is marked as `pronoun`.
* For the sentence `This Fallujah operation my turn out to be the most important operation done by the US Military since the end of the war.`
  * The word `US` should be `noun` but it is marked as `pronoun`.
