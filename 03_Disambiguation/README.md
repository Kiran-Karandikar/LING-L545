<!-- toc -->

## Table of contents

-   [Improve perceptron tagger](#improve-perceptron-tagger)
-   [Feature Engineering `tagger.py`.](#feature-engineering-taggerpy)

<!-- tocstop -->
# Morphological Disambiguation

## Improve perceptron tagger

The objective of this task is to download and run a very basic averaged
perceptron tagger (less than 300 lines of Python). After successfully running
it, try and improve it by changing the feature specifications.

First download the code:

```shell
git clone https://github.com/ftyers/conllu-perceptron-tagger.git
```
for purpose of this assignment we will be using the corpus for english language.

```shell
git clone https://github.com/UniversalDependencies/UD_English-EWT.git
```

Then download the CoNLL shared task 2017 official evaluation script and unzip
it:

```shell
wget http://universaldependencies.org/conll17/eval.zip
unzip eval.zip
cd conllu-perceptron-tagger
```

You can train the tagger using the following command:

```shell
cat ../UD_English-EWT/en_ewt-ud-train.conllu | python3 tagger.py -t pt-ud.dat
```

Now you can run the tagger:

```shell
cat ../UD_English-EWT/en_ewt-ud-test.conllu | python3 tagger.py pt-ud.dat > pt-ud-test.out
```

And evaluate:

```shell
python3 ../evaluation_script/conll17_ud_eval.py --verbose ../UD_English-EWT/en_ewt-ud-test.conllu pt-ud-test.out
```

## Feature Engineering `tagger.py`.

Before making the changes the baseline performance on `en_ewt-ud-dev.conllu` was as follows.

```text
Metrics    | Precision |    Recall |  F1 Score | AligndAcc
-----------+-----------+-----------+-----------+-----------
Tokens     |    100.00 |    100.00 |    100.00 |
Sentences  |    100.00 |    100.00 |    100.00 |
Words      |    100.00 |    100.00 |    100.00 |
UPOS       |     93.70 |     93.70 |     93.70 |     93.70
XPOS       |    100.00 |    100.00 |    100.00 |    100.00
Feats      |    100.00 |    100.00 |    100.00 |    100.00
AllTags    |     93.70 |     93.70 |     93.70 |     93.70
Lemmas     |    100.00 |    100.00 |    100.00 |    100.00
UAS        |    100.00 |    100.00 |    100.00 |    100.00
LAS        |    100.00 |    100.00 |    100.00 |    100.00
```

In general, the 'tagger.py' file generates features in two steps: first, it
retrieves the current sentence, normalizes it, and then generates relevant
features.

Initially, an attempt was made to change the way sentences/words are normalized
by modifying the code in method: 'def _normalise(self, word)'.
It was discovered during the initial analysis of train data that the train data
contains multiple stop words, data related to calendar months, US states, weight
and length quantities.

Thus, the first attempt was to normalize by creating a list of words that needed
to be omitted or masked, as shown below.

```python
months = {'jun', 'april', 'december', 'aug', 'october', 'jan', 'february', 'dec', 'may', 'mar', 'jul',
                  'september',
                  'apr', 'november', 'nov', 'feb', 'march', 'january', 'august', 'sep', 'july', 'june', 'oct'}
us_states = {'sacramento', 'south', 'alabama', 'california', 'il', 'austin', 'detroit', 'jersey', 'columbia',
             'washington', 'minneapolis', 'york', 'tennessee', 'north', 'sc', 'ms', 'vermont',
             'oregon', 'tx', 'nashville', 'lincoln', 'pa', 'michigan', 'id', 'atlanta', 'nevada', 'fl',
             'jackson', 'in', 'anchorage', 'wv', 'maine', 'ca', 'tn', 'denver', 'connecticut', 'dover', 'az',
             'baltimore', 'rock', 'hartford', 'city', 'ri', 'va', 'louisiana', 'juneau', 'ia', 'me', 'los',
             'augusta', 'ct', 'arkansas', 'bismarck', 'milwaukee', 'cheyenne', 'mt', 'houston', 'baton', 'ut',
             'co', 'jacksonville', 'nj', 'billings', 'ma', 'wyoming', 'ar', 'idaho', 'hi', 'boise', 'or', 'ne',
             'texas', 'md', 'helena', 'virginia', 'west', 'al', 'olympia', 'boston', 'massachusetts',
             'georgia',
             'ok', 'rouge', 'omaha', 'montgomery', 'honolulu', 'minnesota', 'island', 'richmond', 'hawaii',
             'ga', 'seattle', 'ohio', 'little', 'wi', 'nebraska', 'ak', 'topeka', 'oh', 'kentucky',
             'wisconsin',
             'salem', 'providence', 'iowa', 'birmingham', 'springfield', 'charleston', 'la', 'de',
             'wilmington',
             'mississippi', 'lake', 'philadelphia', 'burlington', 'bridgeport', 'maryland', 'nd', 'mn',
             'oklahoma', 'phoenix', 'utah', 'nv', 'ks', 'annapolis', 'indianapolis', 'dakota',
             'angelescolorado', 'kansas', 'mexico', 'portland', 'ky', 'montpelier', 'sd', 'moines', 'wa',
             'chicago', 'delaware', 'harrisburg', 'salt', 'nc', 'new', 'indiana', 'concord', 'albany',
             'madison', 'florida', 'wy', 'mo', 'lansing', 'columbus', 'vt', 'des', 'trenton', 'montana', 'mi',
             'nm', 'missouri', 'nh', 'jefferson', 'raleigh', 'ny', 'arizona', 'pierre', 'louisville',
             'illinois', 'carson', 'carolina', 'wichita', 'rhode', 'pennsylvania', 'santa', 'alaska',
             'hampshire', 'frankfort', 'tallahassee'}
stop_words = {'to', "isn't", 'will', 'having', "don't", 'of', 'then', "aren't", 'but', 'was', 'she', 'until',
              'couldn', 'we', 'were', 'being', 'same', 'who', 'out', 'wouldn', 'now', "mightn't", 'both',
              'further', 'ours', 'where', "it's", 'against', 'our', 'doing', 'mustn', 'himself', 'have', 'any',
              'few', 'haven', 'at', 'while', "wouldn't", 'doesn', 'more', 'been', "needn't", "you'd",
              "should've", 'wasn', 're', 'ma', 'such', 'other', 'o', 'their', 'this', 'so', 'why', 'on',
              "she's", 'a', 'each', 'over', 'here', 'm', 'too', 'weren', 'for', 'off', 'how', "weren't",
              'because', 'hers', 'in', 'just', 'if', 'nor', 'i', 'my', "that'll", 'there', 'they', "won't",
              'did', 'again', "didn't", 'an', 'themselves', 'those', 'down', "hadn't", "you're", 'all', 'what',
              'does', 'be', 'than', 'most', 've', 'is', 'or', 'about', 'it', 'hasn', 'them', 'under',
              'ourselves', 'your', 'are', 'he', 'no', 'as', 'from', 'own', "doesn't", 'y', 'myself', 'with',
              's', 'won', 'isn', 'his', 'up', 'theirs', 'once', 'between', 'had', 'am', 'when', 'needn',
              'whom',
              'd', "you'll", 'by', "couldn't", 'can', 'these', 'during', 'and', "mustn't", "you've",
              'yourself',
              'before', 'aren', 'should', 'through', 'her', 't', "shouldn't", 'yourselves', 'mightn', 'yours',
              'didn', 'me', 'some', 'shouldn', 'herself', "wasn't", 'don', 'only', 'shan', 'above', 'not',
              'you', 'very', 'hadn', 'itself', 'the', 'him', 'has', "hasn't", 'which', "haven't", 'after',
              "shan't", 'its', 'll', 'below', 'ain', 'into', 'do', 'that'}
```

and is here change code snippet.

```python
# original code
if '-' in word and word[0] != '-':
    return "!HYPHEN"
elif word.isdigit() and len(word) == 4:
    return "!YEAR"
elif word[0].isdigit():
    return "!DIGITS"
elif word.lower() in months:
    return "!MONTH"
elif word.lower() in us_states:
    return "!US_STATE"
elif word.lower in stop_words:
    return "!STOP_WORD"
else:
    return word.lower()
```

Running multiple iterations with these changes and adding or removing these
features resulted in no improvement in performance over the baseline.

The outcomes of these attempts are shown below.

```text
# Using `months` and `us_states` data.

Metrics    | Precision |    Recall |  F1 Score | AligndAcc
-----------+-----------+-----------+-----------+-----------
Tokens     |    100.00 |    100.00 |    100.00 |
Sentences  |    100.00 |    100.00 |    100.00 |
Words      |    100.00 |    100.00 |    100.00 |
UPOS       |     93.59 |     93.59 |     93.59 |     93.59
XPOS       |    100.00 |    100.00 |    100.00 |    100.00
Feats      |    100.00 |    100.00 |    100.00 |    100.00
AllTags    |     93.59 |     93.59 |     93.59 |     93.59
Lemmas     |    100.00 |    100.00 |    100.00 |    100.00
UAS        |    100.00 |    100.00 |    100.00 |    100.00
LAS        |    100.00 |    100.00 |    100.00 |    100.00
```

```text
# Using `months`,`us_states` and `stop_words` data.

Metrics    | Precision |    Recall |  F1 Score | AligndAcc
-----------+-----------+-----------+-----------+-----------
Tokens     |    100.00 |    100.00 |    100.00 |
Sentences  |    100.00 |    100.00 |    100.00 |
Words      |    100.00 |    100.00 |    100.00 |
UPOS       |     93.53 |     93.53 |     93.53 |     93.53
XPOS       |    100.00 |    100.00 |    100.00 |    100.00
Feats      |    100.00 |    100.00 |    100.00 |    100.00
AllTags    |     93.53 |     93.53 |     93.53 |     93.53
Lemmas     |    100.00 |    100.00 |    100.00 |    100.00
UAS        |    100.00 |    100.00 |    100.00 |    100.00
LAS        |    100.00 |    100.00 |    100.00 |    100.00
```

Since no progress was being made, the focus was shifted to changing how features
are generated in method:' def _get features(self, I word, context, prev, prev2)'.

Changes were first made to the way suffixes were handled, specifically for following code snippet.

```python
add('i suffix', word[-3:])
add('i-1 suffix', context[i - 1][-3:])
add('i+1 suffix', context[i + 1][-3:])
```

Following several test runs, a slight improvement in performance was seen using
the following.

```python
add('i suffix', word[-2:])
add('i-1 suffix', context[i - 1][-2:])
add('i+1 suffix', context[i + 1][-2:])
```

The outcomes of these attempts are shown below:

```text
# Changes to normalization + using suffix as lst 4 chars in given word

Metrics    | Precision |    Recall |  F1 Score | AligndAcc
-----------+-----------+-----------+-----------+-----------
Tokens     |    100.00 |    100.00 |    100.00 |
Sentences  |    100.00 |    100.00 |    100.00 |
Words      |    100.00 |    100.00 |    100.00 |
UPOS       |     93.41 |     93.41 |     93.41 |     93.41
XPOS       |    100.00 |    100.00 |    100.00 |    100.00
Feats      |    100.00 |    100.00 |    100.00 |    100.00
AllTags    |     93.41 |     93.41 |     93.41 |     93.41
Lemmas     |    100.00 |    100.00 |    100.00 |    100.00
UAS        |    100.00 |    100.00 |    100.00 |    100.00
LAS        |    100.00 |    100.00 |    100.00 |    100.00
```

```text
# Using suffix as last 4 chars in given word

Metrics    | Precision |    Recall |  F1 Score | AligndAcc
-----------+-----------+-----------+-----------+-----------
Tokens     |    100.00 |    100.00 |    100.00 |
Sentences  |    100.00 |    100.00 |    100.00 |
Words      |    100.00 |    100.00 |    100.00 |
UPOS       |     93.49 |     93.49 |     93.49 |     93.49
XPOS       |    100.00 |    100.00 |    100.00 |    100.00
Feats      |    100.00 |    100.00 |    100.00 |    100.00
AllTags    |     93.49 |     93.49 |     93.49 |     93.49
Lemmas     |    100.00 |    100.00 |    100.00 |    100.00
UAS        |    100.00 |    100.00 |    100.00 |    100.00
LAS        |    100.00 |    100.00 |    100.00 |    100.00
```

```text
# Using suffix as last 2 chars in given word

Metrics    | Precision |    Recall |  F1 Score | AligndAcc
-----------+-----------+-----------+-----------+-----------
Tokens     |    100.00 |    100.00 |    100.00 |
Sentences  |    100.00 |    100.00 |    100.00 |
Words      |    100.00 |    100.00 |    100.00 |
UPOS       |     93.51 |     93.51 |     93.51 |     93.51
XPOS       |    100.00 |    100.00 |    100.00 |    100.00
Feats      |    100.00 |    100.00 |    100.00 |    100.00
AllTags    |     93.51 |     93.51 |     93.51 |     93.51
Lemmas     |    100.00 |    100.00 |    100.00 |    100.00
UAS        |    100.00 |    100.00 |    100.00 |    100.00
LAS        |    100.00 |    100.00 |    100.00 |    100.00
```

The term that follows the current word was then treated differently, as was the
prefix for the specified word. After numerous test runs, adding the following
features to the current set of features led to an improvement in performance.

```python
add('i pref1', word[:3])
add('i+1 word pref1', context[i + 1][:3])
```
The outcomes of these attempts are shown below:

```text

# Using `add('i pref1', word[:2])` and add('i+1 word pref1', context[i + 1][0])`

Metrics    | Precision |    Recall |  F1 Score | AligndAcc
-----------+-----------+-----------+-----------+-----------
Tokens     |    100.00 |    100.00 |    100.00 |
Sentences  |    100.00 |    100.00 |    100.00 |
Words      |    100.00 |    100.00 |    100.00 |
UPOS       |     93.52 |     93.52 |     93.52 |     93.52
XPOS       |    100.00 |    100.00 |    100.00 |    100.00
Feats      |    100.00 |    100.00 |    100.00 |    100.00
AllTags    |     93.52 |     93.52 |     93.52 |     93.52
Lemmas     |    100.00 |    100.00 |    100.00 |    100.00
UAS        |    100.00 |    100.00 |    100.00 |    100.00
LAS        |    100.00 |    100.00 |    100.00 |    100.00

```

```text

#  Using `add('i pref1', word[:2])` and add('i+1 word pref1', context[i + 1][:2])`

Metrics    | Precision |    Recall |  F1 Score | AligndAcc
-----------+-----------+-----------+-----------+-----------
Tokens     |    100.00 |    100.00 |    100.00 |
Sentences  |    100.00 |    100.00 |    100.00 |
Words      |    100.00 |    100.00 |    100.00 |
UPOS       |     93.65 |     93.65 |     93.65 |     93.65
XPOS       |    100.00 |    100.00 |    100.00 |    100.00
Feats      |    100.00 |    100.00 |    100.00 |    100.00
AllTags    |     93.65 |     93.65 |     93.65 |     93.65
Lemmas     |    100.00 |    100.00 |    100.00 |    100.00
UAS        |    100.00 |    100.00 |    100.00 |    100.00
LAS        |    100.00 |    100.00 |    100.00 |    100.00

```


```text

#  Using `add('i pref1', word[:3])` and add('i+1 word pref1', context[i + 1][:3])`

Metrics    | Precision |    Recall |  F1 Score | AligndAcc
-----------+-----------+-----------+-----------+-----------
Tokens     |    100.00 |    100.00 |    100.00 |
Sentences  |    100.00 |    100.00 |    100.00 |
Words      |    100.00 |    100.00 |    100.00 |
UPOS       |     93.73 |     93.73 |     93.73 |     93.73
XPOS       |    100.00 |    100.00 |    100.00 |    100.00
Feats      |    100.00 |    100.00 |    100.00 |    100.00
AllTags    |     93.73 |     93.73 |     93.73 |     93.73
Lemmas     |    100.00 |    100.00 |    100.00 |    100.00
UAS        |    100.00 |    100.00 |    100.00 |    100.00
LAS        |    100.00 |    100.00 |    100.00 |    100.00
```

The results of testing these changes against `en_ewt-ud-test.conllu` are shown
below.

```shell
$ cat ../UD_English-EWT/en_ewt-ud-train.conllu | python3 tagger.py -t pt-ud.dat

207227
Iter 0: 185778/207227=89.64951478330526
207182
Iter 1: 193606/207227=93.42701481949746
207189
Iter 2: 197633/207227=95.37029441144253
207217
Iter 3: 199884/207227=96.45654282501798
207201
Iter 4: 201374/207227=97.17556109966365
```
```shell
$ cat ../UD_English-EWT/en_ewt-ud-test.conllu | python3 tagger.py pt-ud.dat > pt-ud-test.out
```
and

```shell
$ python3 ../evaluation_script/conll17_ud_eval.py --verbose ../UD_English-EWT/en_ewt-ud-test.conllu pt-ud-test.out

Metrics    | Precision |    Recall |  F1 Score | AligndAcc
-----------+-----------+-----------+-----------+-----------
Tokens     |    100.00 |    100.00 |    100.00 |
Sentences  |    100.00 |    100.00 |    100.00 |
Words      |    100.00 |    100.00 |    100.00 |
UPOS       |     93.82 |     93.82 |     93.82 |     93.82
XPOS       |    100.00 |    100.00 |    100.00 |    100.00
Feats      |    100.00 |    100.00 |    100.00 |    100.00
AllTags    |     93.82 |     93.82 |     93.82 |     93.82
Lemmas     |    100.00 |    100.00 |    100.00 |    100.00
UAS        |    100.00 |    100.00 |    100.00 |    100.00
LAS        |    100.00 |    100.00 |    100.00 |    100.00
```
