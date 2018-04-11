
# Instant Data Science

When starting any course, you likely look at the syllabus to see what's covered and ask yourself if you can do it. In this lesson, we'll hope to give you a sense of how, with just a little bit of knowledge, you can make some real progress in using programs to answer questions with data.  

To do so, we will be introducing the following topics: 
* Data types: working with text and data 
* Variables: storing data
* Lists: working with data in an ordered collection
* Dictionaries: representing data as a collection of attributes   
* Loops and iteration: repeating a sequence of instructions  
* Data visualization: using plots to display data
* Functions: defining and running specific procedures in code 

This lesson will offer a brief glimpse into each of these topics.  In the rest of the course, we will provide lessons and labs on each of these topics to break down the material step by step.  

### Song Analysis

What makes a hit record?  Does repetitiveness help?  Is our music getting more repetitive over time?  Questions like these were asked by the great computer scientist Donald Knuth in 1977, and then they were reasked and answered, by Colin Morris in [this article](https://pudding.cool/2017/05/song-repetition/).

Here is a chart that Colin Morris produced showing some of the most repetitive popular artists.  How was something like this made and calculated?

![](https://learn-verified.s3.amazonaws.com/data-science-assets/song-chart.png)

### Analyzing one song

Let's take the song *Barbara Ann*, the most repetitive song of the Beach Boys which was remastered by the cast of *Saved by the Bell* in 1990.  

![](https://learn-verified.s3.amazonaws.com/data-science-assets/saved-by-bell.gif)

How did the cast learn all of the words so easily?  Repetition. Here are some of the lyrics.

    Ah, ba ba ba ba Barbara Ann
    Ba ba ba ba Barbara Ann

    Oh Barbara Ann take my hand
    Barbara Ann
    You got me rockin' and a-rollin'
    Rockin' and a-reelin'
    Barbara Ann ba ba
    Ba Barbara Ann

    ...more lyrics...

    Ba ba ba ba Barbara Ann
    Ba ba ba ba Barbara Ann

It keeps going, but you get the point.  Now let's say that we wanted to count up how many times each word in the above selection appears.  Without a computer, we could do the following: 

* Place each of the words on a separate index card
* Designate a spot for each unique word in our index cards
* Then, flip through the index cards one by one
* While flipping through each index card, find its designated pile and increase the size by one


Let's call these steps above **our plan**.  At the end of this lesson and after completing each step of our above plan, we will have a chart, like the one below, giving us a visualization of the most repitious words in the Beach Boys' song, *Barbara Ann*. 

![](https://s3.amazonaws.com/learn-verified/data-science-assets/beach_boys_repitition_chart.png)

Great! Now let's translate our plan into code and make our chart!

### Strings and Variables

To solve this problem with code, we do something similar.  We start with our words in a **string**, which is a data structure that represents text.  This is how it looks:


```python
"Ah, Ba Ba Ba Ba Barbara Ann Ba Ba Ba Ba Barbara Ann Oh Barbara Ann Take My Hand Barbara Ann You Got Me Rockin' And A-Rollin' Rockin' And A-Reelin' Barbara Ann Ba Ba Ba Barbara Ann ...More Lyrics... Ba Ba Ba Ba Barbara Ann Ba Ba Ba Ba Barbara Ann"
```




    "Ah, Ba Ba Ba Ba Barbara Ann Ba Ba Ba Ba Barbara Ann Oh Barbara Ann Take My Hand Barbara Ann You Got Me Rockin' And A-Rollin' Rockin' And A-Reelin' Barbara Ann Ba Ba Ba Barbara Ann ...More Lyrics... Ba Ba Ba Ba Barbara Ann Ba Ba Ba Ba Barbara Ann"



> **Note:** What you see above in the first gray box is Python code.  The content in this box is the code you would write.  What comes below this first box is the **output** of running the code.  So the output of creating a string, is just that same string - not very interesting. 

To create a **string** in Python, notice that we place quotes at the start and end of text.  If we don't do this, Python will give us an error.

So, to avoid errors, we need quotes around our text to make a string, but to hold on to this string and reference it later, we assign it to a variable.  


```python
lyrics = "Ah, Ba Ba Ba Ba Barbara Ann Ba Ba Ba Ba Barbara Ann Oh Barbara Ann Take My Hand Barbara Ann You Got Me Rockin' And A-Rollin' Rockin' And A-Reelin' Barbara Ann Ba Ba Ba Barbara Ann ...More Lyrics... Ba Ba Ba Ba Barbara Ann Ba Ba Ba Ba Barbara Ann"
```

Now whenever we type the word `lyrics` into Python we reference our string.

```python 
lyrics
```

```python
"Ah, Ba Ba Ba Ba Barbara Ann Ba Ba Ba Ba Barbara Ann Oh Barbara Ann Take My Hand Barbara Ann You Got Me Rockin' And A-Rollin' Rockin' And A-Reelin' Barbara Ann Ba Ba Ba Barbara Ann ...More Lyrics... Ba Ba Ba Ba Barbara Ann Ba Ba Ba Ba Barbara Ann"
```

Okay, great. We now have our lyrics assigned to our variable, `lyrics` and we can use that to reference the string later in our code.  If we remember **our plan**, the first step was to place each word on a separate index card, but strings are **not** good at separating our text into individual words.  For that, we need a new data structure called a **list**.

### Lists

To separate our string into a list of individual words, we need to change this continuous string into a Python `list`.  Here is how we tell the computer to do this: split the string into a different entity every time you see a space.  Here are those directions in code.


```python
list_of_lyrics = lyrics.split(' ')
```

Ok, let's see what `list_of_lyrics` looks like.  You're about to see a lot of words, so just scroll through them, and we'll meet up afterwards.

```python 
list_of_lyrics
```

```python
['Ah,', 'Ba', 'Ba', 'Ba', 'Ba', 'Barbara', 'Ann', 'Ba', 'Ba', 'Ba', 'Ba', 'Barbara', 'Ann', 'Oh', 'Barbara', 'Ann', 'Take', 'My', 'Hand', 'Barbara', 'Ann', 'You', 'Got', 'Me', "Rockin'", 'And', "A-Rollin'", "Rockin'", 'And', "A-Reelin'", 'Barbara', 'Ann', 'Ba', 'Ba', 'Ba', 'Barbara', 'Ann', '...More', 'Lyrics...', 'Ba', 'Ba', 'Ba', 'Ba', 'Barbara', 'Ann', 'Ba', 'Ba', 'Ba', 'Ba', 'Barbara', 'Ann']
```

Ok, so this is a `list`. It's an ordered collection, and as you can see we are now treating each word as an individual **entity**. Each individual entity of a list is called an element. How many elements are there in this `list`?


```python
len(list_of_lyrics)
```




    51



Ok, but remember the second step of our plan was to allocate space for each unique word. Now that we have a list of all words, let's make a list of the unique words.

```python
unique_words = set(list_of_lyrics)
```

```python
{'...More', "A-Reelin'", "A-Rollin'", 'Ah,', 'And', 'Ann', 'Ba', 'Barbara', 'Got', 'Hand', 
 'Lyrics...', 'Me', 'My', 'Oh', "Rockin'", 'Take', 'You'}
```

Ok, you may have noticed that our list of unique words is significantly smaller than our total list of words.  How much smaller?


```python
len(unique_words)
```




    17



A lot.

So, there's a lot of repetition in `Barbara Ann`.  It's time to keep track of each word and the number of occurrences of each word.

### Using dictionaries

Our ultimate goal is to present our list of repetitions almost as a table, with a word to the left and the number of occurrences to the right.  

| Word        | Count           |
| ------------- |:-------------:|
| Ann     | 2 |
| Barbara     | 3 |
| Ba     | 8 |

In Python, this looks like a dictionary.


```python
word_counts =  {'Ann': 2, 'Barbara': 3, 'Ba': 8}
```

A dictionary is a collection of key-value pairs which we use to store associated data. Here, each word is associated with its count, and we can use the key to access the associated value.


```python
word_counts['Ann']
```




    2



We can also use the key to reassign that value.


```python
word_counts['Ann'] = 33
```


```python
word_counts
```




    {'Ann': 33, 'Ba': 8, 'Barbara': 3}



So that's the form we want. How do we get there with our list of lyrics?

Well we start by creating a dictionary with each key as a separate word, and then set the corresponding value to zero.  Kind of like allocating a region on a table for each of our words.  We do this with the `unique_words` list and the `fromkeys` method, whose second argument is the value we set for each key.

```python 
word_histogram = dict.fromkeys(unique_words, 0)
```

```python
{'...More': 0, "A-Reelin'": 0, "A-Rollin'": 0, 'Ah,': 0, 'And': 0, 'Ann': 0, 'Ba': 0, 'Barbara': 0, 'Got': 0, 'Hand': 0, 'Lyrics...': 0, 'Me': 0, 'My': 0, 'Oh': 0, "Rockin'": 0, 'Take': 0, 'You': 0}
```

### Loops

Ok, now we have two nice data structures. A `list_of_lyrics` of all of our words, and a `word_histogram` to keep track of the amount of words. It seems like we're making good progress. Let's look again at our plan.

* Place each of the words on a separate index card. 
    * **Complete** as `list_of_lyrics`
* Allocate space for a small pile for each unique word
    * **Complete** as `word_histogram`
* Then, go through the index cards one by one
* And for each index card, increase the size of its related pile by one


So looking through the steps, all that's left are the last two steps.

In Python, to go through elements of a list one by one, we use a `for` loop.


```python
for number in [1,2,3,4]:
    print(number + 10)
```

    11
    12
    13
    14


Ok, so here we want to go through the elements of our `list_of_lyrics` one by one. For each word in `list_of_lyrics`, we want to find the related key in the dictionary, `word_histogram`, and increase the value by one. So now, instead of looping through a list of numbers, we will loop through each of our words in `list_of_lyrics`, find the related value in the dictionary, and increase it by one.

> **Deep breath** These next lines of code may look like magic.  The lessons that follow will explain them.


```python
word_histogram = dict.fromkeys(unique_words, 0)
for word in list_of_lyrics:
    word_histogram[word] = word_histogram[word]+ 1 
```

> We said it would be confusing.  Good thing there are more lessons to explain it.  Let's see if it worked.

```python
word_histogram
```

```python
{'...More': 1, "A-Reelin'": 1, "A-Rollin'": 1, 'Ah,': 1, 'And': 2, 'Ann': 8, 'Ba': 19, 'Barbara': 8, 'Got': 1, 
 'Hand': 1, 'Lyrics...': 1, 'Me': 1, 'My': 1, 'Oh': 1, "Rockin'": 2, 'Take': 1, 'You': 1}
```

Ok, that's it.  Now if we want to see how many times 'Rockin' appears, we can do so easily.


```python
word_histogram["Rockin'"]
```




    2



### Visualizing the data

We've got our answer in code.  The final step is to turn it into a chart.  We'll use a library -- which is a collection of code we get from the Internet that does not come with Python -- called Plotly to make our charts. 

In the first four lines we tell Python to get ready to use this library.  And in the last line we tell Python to plot our `trace`.

The meat of the code is our `trace`.  A trace points to a dictionary with a key of `x` that points to a list of x_values, and a key of `y` that points to y_values.  And a `type` to indicate that this will be a bar chart.

```python
import plotly
from plotly.offline import iplot, init_notebook_mode
from plotly import tools
import plotly.graph_objs as go
init_notebook_mode(connected=True)


trace = {
    'type': 'bar', 
    'x': list(unique_words), 
    'y': list(word_histogram.values())
    }

plotly.offline.iplot({'data': [trace]})
```

![](https://s3.amazonaws.com/learn-verified/data-science-assets/beach_boys_repitition_chart.png)

Above we can see that `x` points to a `list` of the `unique_words`, and `y` points to the `list` of values from our `word_histogram`, which represent the number of times each word appears. 

We now have plotted our words. The Beach Boys say "Ba" 19 times and remember we only copied over some of the lyrics.  Repetitive indeed.

### Summary

In the first twenty lessons, we will cover these topics and more. Hopefully, in this section you can see that even with just a bit of knowledge we can really put code to use. It may have seemed like a lot of work, but the work was in the learning, not the code.  

All of the code written so far was really just six lines of code plus another 8 lines to plot our chart, giving us a grand total of a mere 14 lines of code! 

These next sections will go through each of the topics we introduced in this lesson, so that we can begin use the tools above to explore information with code.
