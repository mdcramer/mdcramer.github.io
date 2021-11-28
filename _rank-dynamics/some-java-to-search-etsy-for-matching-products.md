---
title: "Some Java to Search Etsy for Matching Products"
date: "2014-01-16"
tags: 
  - "code"
---

To put together a [demonstration of Surf Canyon's search technology with Etsy's products](http://etsyi.surfcanyon.com "Etsy Demonstration"), we needed some Java code that would search Etsy and return a list of matching products.  We assumed that this could probably be done in about 100 lines of Java code.

We also figured someone must have done this before, but after searching online the code that we found was much longer and a lot more complicated (mainly because it was trying to access parts of the Etsy API that required OAuth authentication) than what we had been expecting. However, just doing a product search doesn't require any authentication, so we went ahead and wrote some much simpler code that did only what we needed.

The Java code, written by [Mike Wertheim](http://www.surfcanyon.com/team.jsp "Surf Canyon Team"), is about 100 lines long and can be found at [http://www.surfcanyon.com/EtsyListingFetcher.jsp](http://www.surfcanyon.com/EtsyListingFetcher.jsp).

The code makes use of Jackson (an open source Java library that handles JSON).  To compile and run, download the two Jackson jar files ([http://repo1.maven.org/maven2/org/codehaus/jackson/jackson-core-asl/1.9.13/jackson-core-asl-1.9.13.jar](http://repo1.maven.org/maven2/org/codehaus/jackson/jackson-core-asl/1.9.13/jackson-core-asl-1.9.13.jar) and [http://repo1.maven.org/maven2/org/codehaus/jackson/jackson-mapper-asl/1.9.13/jackson-mapper-asl-1.9.13.jar](http://repo1.maven.org/maven2/org/codehaus/jackson/jackson-mapper-asl/1.9.13/jackson-mapper-asl-1.9.13.jar)) and put them in your Java CLASSPATH.  Then copy the code from the web page ([http://www.surfcanyon.com/EtsyListingFetcher.jsp](http://www.surfcanyon.com/EtsyListingFetcher.jsp)) to the clipboard and paste it into a file called EtsyListingFetcher.java.  (If you download the code directly, instead of doing copy and paste, you will probably run into problems with HTML entities.)

If you have any questions or feedback, please post them in the comments below or [contact us](http://www.surfcanyon.com/contact.jsp "Contact Surf Canyon").
