---
title: "Back in Action on AMO!"
date: "2015-02-20"
tags: 
  - "announcements"
  - "code"
---

July 17th, 2012 was the last time we were able to successfully update [our browser extension on AMO](https://addons.mozilla.org/en-US/firefox/addon/google-assistant-by-surf-canyo/ "Fast Search by Surf Canyon on AMO"), Mozilla's extension directory. That was version 3.4.3. Many things have obviously happened since then, including new features, bug fixes and optimizations. We're therefore now happy to announce that Surf Canyon version 5.4.0, fully compatible with Firefox 35.0 and capable of being installed without having to restart the browser, was approved on January 14th.

What took so long?

Recently, Firefox has been undergoing a massive architectural change that would result in better security and performance for Firefox. "Electrolysis" (e10s) is a new, multi-process architecture coming in a future release of Firefox. This new architecture separates Firefox's core from open websites. An unfortunate trade-off was that older add-ons weren't guaranteed to be supported. Surf Canyon would no longer run on the newly envisioned Firefox; nor would some of our favorite add-ons, such as "Greasemonkey."

While older add-ons weren't supported, anything written using the Firefox AddOn SDK (formerly known as "Jetpack") were to remain unaffected. In order to stay on Firefox, we rewrote the add-on using the Firefox AddOn SDK. Moving to a new add-on framework, however, meant learning new tricks.  For example, Firefox's AddOn SDK makes Ajax calls somewhat tricky, since only restricted parts of the add-on are able to access the Ajax APIs.  We implemented a "Callback registry" to solve this problem.  If you would like to see the code, we've posted it on [Pastebin](http://pastebin.com/5bKJ2f5P "Firefox SDK Callback Registry").
