
## Exercises with sed

 - Count word initial consonant sequences: tokenise by word, delete the vowel and the rest of the word, and count
 - Count word final consonant sequences

> Language code is : `om`

```bash
# Pattern for initial-consonants.hist

sed 's/[^a-zA-Z]\+/\n/g' < wiki.txt| sort -r | sed -r 's/(^[^aeiouAEIOU]*)([aeiouAEIOU])([a-zA-Z]*)$/\1/p' | sort -r | uniq -c > initial-consonants.hist

# Patter for final-consonants.hist

sed 's/[^a-zA-Z]\+/\n/g' < wiki.txt | sort -r | sed -r 's/^(.*)([aeiouAEIOU])([^aeiouAEIOU]*)$/\3/p' | sort -r | uniq -c > final-consonants.hist
```
