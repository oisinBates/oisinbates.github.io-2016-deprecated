---
layout: post
section-type: post
title: java Word Frequency Counter
category: java
tags: 
---

This project was completed for the University of Limerick module *CS5052 - Programming B*
The module's director set a data mining use case, in which the student's program would read in text, in the format of individual emails, and calculate the 10 most common words used by each email address.

In approaching this problem, I constructed two classes: *Word* and *EmailMapper*.

New *Word* objects can be instantiated with a constructor which requires two parameters: *word* and *count*.The other methods are as follows: *getWord*, *getCount*, *toString*, and *compareTo*. The *compareTo* method compares Word objects based on count and, if count the same, alpabetically & case-insensitively.

The *EmailMapper* class contains a constructor and 4 other methods: *addToEmailWordsMap*, *wordsInFile*, *wordsInLine*,*loadNoiseWords*.

* loadNoiseWords: Loads noise words to a hashset, from a txt file in the project directory.
* wordsInLine: As each line is read, from the txt file to be analysed, *wordsInLine* strips the line of non-alphabetic characters and adds each word to an arrayList.
* wordsInFile: Reads in the txt file of emails and strips away email address and start + finish markers. Creates an arraylist of all words in the email, before passing this ArrayList and email address to the *addToEmailWordsMap* method.
* addToEmailWordsMap: This method adds arraylists and emails to a class variable; a TreeMap called *emailWords* which contains email adress keys mapped to ArrayLists. If the map already contains a key for the email, the existing value is retrieved and both arraylists are added together.
* EmailMapper: The constructor invokes the above methods, filling the *emailWords* TreeMap. It then uses the *Collections.frequency()* java.util method to calculate the most common words for each email address, and prints the top 10 words.

The code for this project can be viewed [on Github](https://github.com/oisinBates/WordFrequencyCounter)
