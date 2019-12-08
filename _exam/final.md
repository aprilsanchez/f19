---
layout: exam_info
num: e03
ready: true
desc: "Final Exam 7:30PM"
exam_date: 2019-12-11 19:30:00.00-7
---

## Exam logistics

Th Final Exam is on **Wednesday, 12/11** in the regular lecture classroom but it starts **at 7:30PM**.

* There will be a seating chart projected on the screen and the TAs will have a physical copy of it, so they'll be able to help you locate your seat.

* You will be given a copy of the exam: you are supposed to work on the copy that you are given and should not trade it with your neighbors. Not following this guideline is considered a violation of academic integrity and can result in receiving a 0 for the exam.

* Bring your **student ID** in case we ask you for it.

* You may bring **only one** 8.5" x 11" piece of paper with _handwritten_ notes on both sides (you don't have to use both sides, but you may if you want to do so). You are **not allowed two sheets** each with one side of notes.
  * Handwritten notes also mean that you should not print anything and/or tape it to your note sheet: research has shown that to best digest the material and understand what you are doing you need to hand-write the notes yourself. 
  * Please write your name in the **top right corner** (portrait orientation) on **both** sides of that sheet.
  * **Do not attach** anything to your notesheet: you will need to turn in your notesheet with your exam. If something is glued/taped/stapled/attached in any way to it, it will jam up the scanner and will cause you to lose points for not following instructions.
  * Rememeber to **turn in your exam and notesheet _before_** you leave the exam room. We will not accept it once you leave the classroom.
  * If you do not need/want to create a notesheet, please turn in a blank sheet with your name in the **top right corner (portrait orientation) on both sides** of that sheet.

*    No books, calculators, phones, laptops or other materials or devices are allowed during the exam. Using them during the exam are a violation of academic integrity and can result in receiving a 0 for the exam.

* You may turn in your exam and the notesheet early. Have all of your belongings with you when you turn in your exam so that as soon as you hand it to us you can leave the classroom immediately, without needing to back to your seat.

*    There are no makeups for this exam.

* * *

Guidelines last updated: Sunday, Dec 8, 2019

* * * 

### Practice Problems

**Look over the clicker questions on the slides, Exam 1 and Exam 2, and homework problems to make sure you know and understand those _concepts_ not just the answers to those specific questions.**

Below are some practice problems -- solve them on paper first, before trying them out in IDLE.

* Write a function `reverse(myStr)` which takes a string as input and recursively reverses it. Recall that to write a recursive function you must call the function from inside of the function.

* Write a function `reverse(myStr)` which takes a string and reverses it by any method you wish.

* Consider the following code segment:

```python
import pytest

def test_perimRect_1():
   assert perimRect(4,5)==18

def test_perimRect_2():
   assert perimRect(7,3)==20

def test_perimRect_3():
   assert perimRect(2.1,4.3)==pytest.approx(12.8)
```

Notice that the third test case above uses `pytest.approx()`. Why is this required for this test case, but not for the first two?


* Assume you are at the command line:

  * How do you display the contents of your current directory?
  * How do you go to your home directory?
  * Make a directory called `cs8` in your current directory?
  * How to change into the directory `cs8` you just created?
  * What are you accessing when you use import?
  * What are you accessing when you use `from some_thing import another_thing`?
  
  

*  Which one/ones of the following operations could not form the string “aabaababds”?

```python
A. “aab”+ “aab”+ “abd” + “s”
B. s=“aabaababdc”, s[-1]= “s”
C. “aabaababdsabc”- “abc”
D. “aab”*2+ “abds”
```

* Write a function `printInput()` to take in an input from the user with the string `“Please type your input\n”` and prints whatever the user typed in.

* Here is the definition of a function, which of the following calls of this function is illegal?
```python
       def multiply(a,b):
             return a*b

A. multiply(123,2)
B. multiply(“123”,2)
C. multiply(“123”, “2”)
D. multiply([1,2,3],2)
```

* Find the line below that has syntax error:

```python
1          def hasZero(num):
2                tostr=str(num)
3                for i in range(len(tostr)):
4                     if(tostr(i)= “0”):
5                         return True
6                return false
```

* Math Time! Write out the order in which the operators will be evaluated and the result of each expression:
```python
       20 // 3 / 3 % 3 = ?
```

Answer:
```
20 // 3 = 6
...
```

* Write down the Truth Table for `and` and `or` operators.

```
T and T → 

T and F → 

F and F → 

T or T → 

T or F → 

F or F → 
```

* Given an array of 0s and 1s, write a function to find the maximum number of consecutive 1s in this array. For Example: input `[1,1,1,0,1]` output `3`. Design a pseudocode first and walk through it using arrays `[0]`, `[1]`, `[0,0]`, `[1,0]`, `[1,1]`, etc.

* Given 2 input strings (`s` and `t`), find their difference (output char). 
(all lowercase, and `t` has 1 more character than `s`)
For instance `s = “abc”` and `t = “abdc”`, output should be `d`. 

* Given a non-negative integer `num`, write a recursive function `addDigits()` to **repeatedly** add all its digits until the result has only one digit. For instance, `99 -> 18 -> 9`.

* Find the all the errors on the following code. (Assume that “file.txt” and “out.txt” exist in the current directory)

```python
    def fileIO():
    infile= open("file.txt", "read")
    outfile = open("out.txt","read")
    x= infile.read()
    for i in x:
        if i = '\n':
        continue
        outfile.write(i)
    y = outfile.read()
    for j in y:
        print(j)
    print("Done")
```

* Define a function that takes as input a list of strings. The function should determine the number of occurrences for each word in the list and then output the result into a file  called “out.txt” in the following format : `word count`. Make sure to format the output such that the count is right aligned and there is a padding of 10 places in between the word and the count.

    
* Given a file, ‘words.txt’,  containing a vast amount of unique words (one word per line), write a program that takes as input an integer `n` and a string `startsWith`.
  * The function should select `n` random unique words from the file that begin with the given string `startsWith`. 
  * For a word to be considered to start with the given substring (startWith) it suffices to have the same letters in the same sequence. In other words matches are not case sensitive. For example, given `startWith= ‘as’` the following strings would be considered matches: `“asteroid”, “Astronaut”, “aSterisk”`
  * There is no guarantee that an `n` amount of words that start with startWith can be found in the file. There could be more than `n`, less than `n`, or none at all. 
  * If no words are found in the file return `None` otherwise return a list containing the available words that start with the substring startWith. 
  * Note: In the case where the amount of words matching startWith is less than n then  there are not enough choices to randomly select. The returned words will always contain the same words (but potentially in a different order). 
  
It is helpful to design a pseudocode first, before trying to write down the code.


