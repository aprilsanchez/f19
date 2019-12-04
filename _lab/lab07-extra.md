---
layout: lab
num: lab07_extra
ready: true
desc: "String Formatting and File IO (cont'd)"
assigned: 2019-12-04 09:00am
due: 2019-12-11 08:59am
---

In this lab, you'll get more practice with:

* Testing your functions with pytest
* Using String Formatting
* Reading and processing files

## This lab should be done solo.

## This lab is optional 
... and is designed to help you test and get credit for your previous solution. Additionally, there are slight modifications you can add to your implementation, which will make the resulting output more interesting to analyze.

### You will get credit for the lab only if you use the material we covered in class.
Looking up how to solve a problem counts as a violation of academic integrity, so refrain from doing so and think of ways how what you learned in class can help you solve this problem. Using functions we have not covered in class is a red flag: we are interested in how well you can apply the material that you learned in this class, not in how well you can look up someone else's solution.

# Part 0

If you open and close the file within every function to get the list of words, consider writing a helper function, which you can call instead.

```python
def getAllWords(filename):
    '''
    Returns a list of all words from the given filename.
    '''
```

# Part 1

If you correctly implemented the previous lab, you should be able to run the following test file and pass all tests.

Note that the [input file "the-gift-of-the-magi.txt"](the-gift-of-the-magi.txt) (source: [Gutenberg project](https://www.gutenberg.org/files/7256/7256-h/7256-h.htm)) contains double-quotes and dollar signs, which are not alpha-numeric characters, however, it should not be a problem if you stuck to our original assumption that "the text only contains the `,.!?;` punctuation characters". 

```python
#test_functions.py (lab 07)

import pytest

input_file = "the-gift-of-the-magi.txt"
total_words = 2065
unique_words = 863

def test_totalWords_prophet():
	'''Test totalWords("input1")'''
	from lab07 import totalWords
	assert totalWords(input_file) == total_words

# Tests for longestWord
def test_longestWord_prophet():
	'''Test longestWord(input1)'''
	from lab07 import longestWord
	assert longestWord(input_file) == "sterling—something"


def test_charactersPerWord_prophet():
	'''Test charactersPerWord(input1)'''
	from lab07 import charactersPerWord
	assert round(charactersPerWord(input_file), 5) == 4.27167

def test_mostCommomWords_1():
	''' Test mostCommomWords, N=1 '''
	from lab07 import mostCommonWords
	assert mostCommonWords(input_file, 1) == ['the']

def test_mostCommomWords_3():
	''' Test mostCommomWords, N=3 '''
	from lab07 import mostCommonWords
	assert mostCommonWords(input_file, 3) == ['the', 'and', 'a']

def test_mostCommomWords_5():
	''' Test mostCommomWords, N=5 '''
	from lab07 import mostCommonWords
	assert mostCommonWords(input_file, 5) == ['the', 'and', 'a', 'of', 'to']

def test_mostCommomWords_30():
	''' Test mostCommomWords, N=30 '''
	from lab07 import mostCommonWords
	words = mostCommonWords(input_file, 30)
	assert words[29] == "out"

def test_mostCommomWords_last():
	''' Test mostCommomWords, last word '''
	from lab07 import mostCommonWords
	words = mostCommonWords(input_file, unique_words)
	assert words[unique_words-1] == "\"Cut"


def test_mostCommomWords_prophet_neg():
	''' Test mostCommomWords, N is negative '''
	from lab07 import mostCommonWords
	assert mostCommonWords(input_file, -1) == None

def test_mostCommomWords_prophet_too_large():
	''' Test mostCommomWords, N is too large '''
	from lab07 import mostCommonWords
	assert mostCommonWords(input_file, unique_words+1) == None
```

# Part 2

Now that you verified that your previous code works as expected, let's add a few modifications to it.

* Let's add double-quotes to the list of symbols we are removing when we read-in the words.
* The lower/upper case or capitalization shouldn't matter when counting words, so let's enforce that by converting words to lowercase. Notice that "hi", "Hi" and "HI" will all be counted as the same word "hi". Dealing with cases like acronyms and state abbreviations is outside the scope of this assignment.

These will be the new tests that you can run if you correctly implemented these modifications.

```python
#test_functions.py (lab 07_extra)
# Without stopwords

import pytest

input_file = "the-gift-of-the-magi.txt"
total_words = 2065
unique_words = 772

def test_totalWords_input1():
	'''Test totalWords("input1")'''
	from lab07_extra import totalWords
	assert totalWords(input_file) == total_words

# Tests for longestWord
def test_longestWord_input1():
	'''Test longestWord(input1)'''
	from lab07_extra import longestWord
	assert longestWord(input_file) == "sterling—something"


def test_charactersPerWord_input1():
	'''Test charactersPerWord(input1)'''
	from lab07_extra import charactersPerWord
	assert round(charactersPerWord(input_file), 5) == 4.24358

def test_mostCommomWords_1():
	''' Test mostCommomWords, N=1 '''
	from lab07_extra import mostCommonWords
	assert mostCommonWords(input_file, 1) == ['the']

def test_mostCommomWords_3():
	''' Test mostCommomWords, N=3 '''
	from lab07_extra import mostCommonWords
	assert mostCommonWords(input_file, 3) == ['the', 'and', 'a']

def test_mostCommomWords_5():
	''' Test mostCommomWords, N=5 '''
	from lab07_extra import mostCommonWords
	assert mostCommonWords(input_file, 5) == ['the', 'and', 'a', 'of', 'to']

def test_mostCommomWords_30():
	''' Test mostCommomWords, N=30 '''
	from lab07_extra import mostCommonWords
	words = mostCommonWords(input_file, 30)
	assert words[29] == "as"

def test_mostCommomWords_last():
	''' Test mostCommomWords, last word '''
	from lab07_extra import mostCommonWords
	words = mostCommonWords(input_file, unique_words)
	assert words[unique_words-1] == "$20"


def test_mostCommomWords_input1_neg():
	''' Test mostCommomWords, N is negative '''
	from lab07_extra import mostCommonWords
	assert mostCommonWords(input_file, -1) == None

def test_mostCommomWords_input1_too_large():
	''' Test mostCommomWords, N is too large '''
	from lab07_extra import mostCommonWords
	assert mostCommonWords(input_file, unique_words+1) == None
```

# Part 3
If you have noticed, the most common words usually include articles and prepositions, which are not very interesting for text analysis.
* Remove stop words using the provided ["stopwords.txt"](stopwords.txt) (source: natural language toolkit (nltk) module)
	* Hint: since `remove` will take out only the first occurrence of an item in the list, you can use a `while` loop and keep removing the item while it is still found in the list.
	* Alternatively, you can create a new list by saving there all words that are not in the list of stopwords.

```python
def removeStopwords(wordList, stopwords_file):
    '''
    Given a list of words (wordList) and a file that
    contains stopwords separated by newlines (stopwords_file),
    remove from wordList all words that are in stopwords_file.
    '''
```

Now that we've added an option to run our code with the stopwords file, let's change our function signatures to add a parameter `stopwords_file`, which by default will be set to `None`.

For example:

```python
def totalWords(filename, stopwords_file = None):
    '''
    Reads the file from filename in your function and returns
    the number of words in the file.
    '''
        allWords = getAllWords(filename)

    if stopwords_file != None:
        allWords = removeStopwords(allWords, stopwords_file)
    else: # stopwords_file is not given
        # do the regular processing

```

Doing so will allow you to run the function with and without the default argument:
* `totalWords(input_file)`
* `totalWords(input_file, stopwords_file)`

Check that adding `stopwords_file = None` to all your functions still works correctly with all the tests from Part 2.


Below are the tests for checking whether the stopwords are being removed correctly.
Notice now that by looking at the top 3 common words you can get a better sense of what this story is about.

```python
#test_functions.py (lab 07_extra)
# With stopwords

import pytest

input_file = "the-gift-of-the-magi.txt"
stopwords_file = "stopwords.txt"
total_words = 1026
unique_words = 660

def test_totalWords_input1_sw():
	'''Test totalWords("input1")'''
	from lab07_extra import totalWords
	assert totalWords(input_file, stopwords_file) == total_words

# Tests for longestWord
def test_longestWord_input1_sw():
	'''Test longestWord(input1)'''
	from lab07_extra import longestWord
	assert longestWord(input_file, stopwords_file) == "sterling—something"


def test_charactersPerWord_sw():
	'''Test charactersPerWord(input1)'''
	from lab07_extra import charactersPerWord
	assert round(charactersPerWord(input_file, stopwords_file), 5) == 5.65107

def test_mostCommomWords_1_sw():
	''' Test mostCommomWords, N=1 '''
	from lab07_extra import mostCommonWords
	assert mostCommonWords(input_file, 1, stopwords_file) == ['jim']

def test_mostCommomWords_3_sw():
	''' Test mostCommomWords, N=3 '''
	from lab07_extra import mostCommonWords
	assert mostCommonWords(input_file, 3, stopwords_file) == ['jim', 'della', 'hair']

def test_mostCommomWords_5_sw():
	''' Test mostCommomWords, N=5 '''
	from lab07_extra import mostCommonWords
	assert mostCommonWords(input_file, 5, stopwords_file) == ['jim', 'della', 'hair', 'said', 'look']

def test_mostCommomWords_30_sw():
	''' Test mostCommomWords, N=30 '''
	from lab07_extra import mostCommonWords
	words = mostCommonWords(input_file, 30, stopwords_file)
	assert words[29] == "time"

def test_mostCommomWords_last_sw():
	''' Test mostCommomWords, last word '''
	from lab07_extra import mostCommonWords
	words = mostCommonWords(input_file, unique_words, stopwords_file)
	assert words[unique_words-1] == "$20"


def test_mostCommomWords_neg_sw():
	''' Test mostCommomWords, N is negative '''
	from lab07_extra import mostCommonWords
	assert mostCommonWords(input_file, -1, stopwords_file) == None

def test_mostCommomWords_too_large_sw():
	''' Test mostCommomWords, N is too large '''
	from lab07_extra import mostCommonWords
	assert mostCommonWords(input_file, unique_words+1, stopwords_file) == None

```



# Upload `{{page.num}}.py` to Gradescope.

Once you're done with writing your functions, navigate to the Lab assignment "{{page.num}}" on Gradescope and upload your `{{page.num}}.py`. 
# `{{page.num}}.py`. 
Remember to add your name and perm number at the start of the file.

