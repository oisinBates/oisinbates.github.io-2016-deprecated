---
layout: post
section-type: post
title: Quick and easy map reduce prototyping with mrjob and AWS Elastic Mapreduce
category: python
tags:
---

Having recently taken an interest in Hadoop, I decided as a learning excerise, to put together a project using Amazon Web Services(AWS). I used [mrjob](https://pythonhosted.org/mrjob/), a Python package which facilitates the user in writing Python programs for use with Hadoop, or in my case, directly with AWS Elastic Mapreduce(EMR). One of the distinct appeals of mrjob, for me, was the ability to test locally without a Hadoop installation. There are some tradeoffs of course: mrjob offers less functionality than other Python frameworks, as well as reduced performance. Having said that, mrjob has an active community, great documentation, and facilitates simple integration with the AWS platform. [Cloudera have an informative blog comparing Python Hadoop frameworks.](http://blog.cloudera.com/blog/2013/01/a-guide-to-python-frameworks-for-hadoop/)

It's said that William Shakespeare [contributed many  new words](https://www.grammarly.com/blog/15-words-invented-by-shakespeare/) to the English language. With this claim in mind, I decided to calculate the occurences of some of these words in a selection of novels/memoirs from [Project Gutenberg](www.gutenberg.org).

Once the user has set up the necessary mrjob config file and downloaded a relevant PEM file from their AWS acount, the entire mapreduce logic was managed in 18 lines of code.(Full source code viewable on [github]())


{% raw %}

	from mrjob.job import MRJob
	import re

	WORD_RE = re.compile(r"[\w']+")

	class MRWordFrequencyCount(MRJob):

	    def mapper(self, _, line):
	        shakespeareWords=["bandit","critic","dauntless","dwindle","elbow","lackluster","lonely","swagger","unaware","uncomfortable","undress","unearthly","unreal"]
	        line=line.lower()
	        for word in WORD_RE.findall(line):
	            if word in shakespeareWords:
	                yield word,1

	        yield "*char_count", len(line)
	        yield "*word_count", len(WORD_RE.findall(line))
	        yield "*line_count", 1

	    def reducer(self, key, values):
	        yield key, sum(values)

	if __name__ == '__main__':
	    MRWordFrequencyCount.run()

{% endraw %}

From the command line, using the above python function, it was possible to analyse the contents of an AWS S3 bucket.


> python [my mrjob function].py -r emr s3://[my S3 bucket]


Though it was tempting to trial the code on **big** data, I opted to keep costs to a minimum and uploaded a humble 14 books(10.5mb in txt format) to the cloud.

With this sample the findings were as follows:

* "*char_count" 10268408
* "*line_count" 203957
* "*word_count" 1875329
* "bandit"    41
* "critic"    7
* "dauntless" 4
* "dwindle"   1
* "elbow"     48
* "lonely"    51
* "swagger"   4
* "unaware"   11
* "uncomfortable" 21
* "undress"   15
* "unearthly" 19
* "unreal"    5
