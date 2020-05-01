# python basics - string manipulation

## import text list from json file
```python
import json
list_name = json.load(open('file_name'))
```
## remove punctuation
```python
import string
def remove_punctuation(text):
    return text.translate(None, string.punctuation)
df['col_name'] = df['col_name'].fillna('')
df['col_name_clean'] = df['col_name'].apply(remove_punctuation)
```

## build word count vector
```python
from sklearn.feature_extraction.text import CountVectorizer
vectorizer = CountVectorizer(token_pattern=r'\b\w+\b') #preserve one letter words
vectorizer_vocabulaty = CountVectorizer(vocabulary = word_list)
feature_matrix = vectorizer.fit(text_list)
```

## sorted word count algorithem
```python
def count_word(s, n):

    all_words = s.split() #break the strings into words
    words_list = sorted(set(all_words)) #removing duplicates and sort in alphabetical order

    words_count_list = []
    for each_unique_word in words_list:
        unique_word_count = all_words.count(each_unique_word)
        words_count_list.append([each_unique_word, unique_word_count])

    sortedWCL = sorted(words_count_list, key = lambda x: x[1], reverse = True)#sort it

    return sortedWCL[:n]#return top N elements the sorted list
```
