---
layout: post
section-type: post
title: Collating and graphin Olympic data with Pandas and Bokeh
category: python 
tags: 
---

I recently came across a [study from the University of Oxford](http://ssrn.com/abstract=2804554) on the costs incured by Olympic host nations. 
As I had been recently looking at the APIs available with the [Pandas](http://pandas.pydata.org/) library, I decided to concantenate some data from the World Bank, alongside the findings of the aforementioned Oxford study.




The World Bank's GDP figures were not available in constant 2015 dollars, so the current rates were used. In contrast, the Oxford study's figures were at the 2015 rate


One risk that I encountered with Pandas was that of reduced precision when working with large numbers.


The graph can be viewed [here]({{ site.url }}assets/olympicspending.html)
