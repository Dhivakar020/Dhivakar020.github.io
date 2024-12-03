---
title: "Browsers Are Weird"
date: 2024-11-27 10:00:00 +0000
categories: Browsers-are-weird
tags: [browsers, Vulnerabilities]
excerpt: "The weird history of browsers that led to security problems"
---

---

> My write-up can be subjective. I understand that not everyone will necessarily agree with my points. Please don’t waste your time trying to prove me wrong, but if you see something really wrong, feel free to let me know.
> {: .prompt-warning }

---

## The Problem: The Weird Nature of Browser Evolution,

Traditional software are usually developed with a fixed set of features defined by the client or the software manufacturer. For instance, consider software like Microsoft Excel. One can trace the steps beginning with conceptualization through all stages of execution and developments and deployment. Once completed, a specific group of customers purchases the software for their personal use. With Excel, people use a spreadsheet to store data-a very dependent variable that works on an individual's specific needs but has the same table-like structure. The whole point i am trying to make here is that traditional software like "Excel" were used locally for personal use.
There is no such thing as "Sharing" in here.

But, in the case of browsers (as a software), they are used to access a common space known as internet. And then comes the major challenge. Contrary to the traditional software approach, various browser vendors gave unique interfaces, which made use of different underlying technologies. The problem here is that different browsers use various technologies but to access the common space with its own integrity. For example, Netscape Navigator 2.0 introduced JavaScript in December 1995, which at that time was not there in other browsers. The real problem arose from the lack of standardization; Every vendor competed to introduce new features in their browsers to gain market share. There was no unified standard that guided the development of browsers in the early stages.

The Computer History Museum encapsulates this dynamic perfectly:

## Browsers: The First Wave (1990–1993)

> Tim Berners-Lee’s 1990 browser-editor ran on rare NeXT computers. CERN refused to fund other versions. So the Web team invited volunteers to write browsers, and provided code to start with.
>
> Eight responded, creating UNIX, Mac, and PC browsers. Viola and Midas were initially the most popular, eclipsed later by Mosaic. Berners-Lee never regained control of his creation.

> The Web’s extraordinary tapestry of images and text is presented to us by web browsers. They are only one component of the Web, along with servers and communications protocols, but they are the most visible.
>
> Whoever writes the dominant browser software decides, by intention or omission, what we can see and do on the Web.

## The Browser Wars

### Browser War 1: Netscape vs. Mosaic

**The Cause:**
Netscape Inc. was initially named as the name Mosaic Communications; however, it moved ahead to an idea whose drawing of a lawsuit on a NCSA on their rights to the name came into being. Naming itself as Netscape had to do the settling.

Early success of Mosaic caught Silicon Valley's eye. In 1994, Jim Clark of Silicon Graphics and Marc Andreessen agreed to a new company venture that aimed at making the "Mosaic killer" browser and server. Netscape had its way quickly in getting Eric Bina and other team members of Mosaic to come aboard and work towards developing the best web browser with great results.

### Browser War 2: Microsoft vs. Netscape

**The Cause:**  
By the mid-1990s, browsers lacked a unified standard. While the internet itself had emerging standards, Tim Berners-Lee addressed this gap in 1994 by founding the World Wide Web Consortium (W3C) at MIT, with a European office in France. According to the Computer History Museum:

> Most of the big "walled gardens" — CompuServe, AOL, Minitel in France—resisted the Web and Internet. They either faded out or ended up as Web sites. Microsoft Network (MSN) might have mounted a serious challenge. But by 1995 the Web was growing quickly, so Microsoft switched course and instead competed on the Web.

In 1995, Microsoft abandoned its MSN-centric strategy and focused on dominating the web with Internet Explorer (IE), which was built on a licensed version of Mosaic. Netscape, buoyed by a record-breaking IPO, initially thrived. However, by 1998, IE had surpassed Netscape in market share. Netscape’s legacy eventually lived on through Firefox, a browser partly inspired by its predecessor.

In a pivotal 1995 memo titled _“Internet Tidal Wave,”_ Bill Gates directed Microsoft’s efforts toward the Web, declaring:

> “I assign the Internet the highest level of importance.”

## Why Security Fell During the Browser War?

#### Speed Over Security:

These two companies, Microsoft and Netscape, were continuously doling out feature releases instead of ensuring something more secure to come first in comparison to its counterpart. In this case, there arose insecurity.

#### Incoherent Standards:

Browsers opted for releasing their own perspective features for being featured in a browser including JavaScript cookies as well as cross-origin sharing so the features may fall into holes so as to create vulnerabilities.

#### Developer Inexperience:

Web developers were just learning how to safely deal with dynamic content, user input, and browser-server interactions.

#### Security Awareness:

An afterthought. Security awareness was very low due to usability and the need to get new functionality out the door as soon as possible.

## Legacy of the Browser Wars,

The browser wars of the 1990s have led to rapid innovation and competition but also laid the groundwork for many web vulnerabilities that are still seen today. This was mainly due to the rushed implementations, inconsistent standards, and a lack of awareness regarding security.
The browser wars of the 1990s accelerated the adoption of the web but left behind an ecosystem riddled with vulnerabilities. Organizations like the W3C, OWASP, and browser vendors introduced standards and best practices over time that have helped mitigate some of these issues. But those seeded during this period continue to influence the security perspective to this day.

## Conclusion,

The intense competition contributed to the rise of vulnerabilities like **XSS, SQLi, CORS issues, CSRF, and SSRF**. In this new series "Browsers are weird", i will write new write-ups explaining how the "Browser Wars" seeded the inevitable vulnerabilities that are still seen today's web applications.

### REFERENCES,

[Computer History Museum](https://www.computerhistory.org/revolution/the-web/20/389)
