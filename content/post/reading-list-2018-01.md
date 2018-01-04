---
title: "Weekly log for 2018, week 01"
description: "My weekly stuff I found interesting to do or read during 2018, week 01 "
date: 2018-01-02T16:42:39+01:00
draft: true
---

This week I've read plenty of stuff about digital accessibility, both from the web developer and application user perspective.

I've recently joined the [Accessible Online Learning Community Group](https://www.w3.org/community/accesslearn/) through my work at [Inria](https://www.inria.fr). This community group focuses on reviewing current <abbr title="World Wide Web Consortium">W3C</abbr> resources and technologies to ensure the requirements for accessible online learning experiences are considered. In other words, the group indentifies what in W3C documents should be patched to meet online learning expectations.

For instance, let's say a teacher needs to use complex images like diagrams or cartoons (some fun won't hurt) in their class. Then they want to publish the class content online so it can be used in a <abbr title="Massive open online course">MOOC</abbr>. Browsing the [web accessibility tutorials](https://www.w3.org/WAI/tutorials/), they find out there are more than one way to do it, but the [Complex Images section](https://www.w3.org/WAI/tutorials/images/complex/) seems to suit the needs. Unfortunately, the given example won't mention anything about _the good way_ to describe flowcharts or cartoons.

This is where <abbr title="Accessible Online Learning Community Group">accesslearn</abbr> comes into play. Its purpose is to find these kind of missing or inadequate information in W3C documentation and propose modifications to the documents. [See the W3C Resources and Gaps Related to Online Learning document](https://docs.google.com/spreadsheets/d/1LHynDV-umVHF3NcKkCIuSL12lzZCj-2qS4gjmLtsXto/edit#gid=1155254872) to figure what the group has identified so far.

Anyway, as I was browsing the accesslearn group archives, I discovered the W3C <abbr title="Education and Outreach Working Group">EOWG</abbr> bound to the <abbr title="Web Accessibility Initiative">WAI</abbr>. A member of this group is [Stéphane Deschamps](https://nota-bene.org/)...

https://cpu.dascritch.net/post/2016/12/14/St%C3%A9phane-Deschamps%2C-Coordinateur-accessibilit%C3%A9-et-open-source-chez-Orange

A discovery leading to another, I dug an interesting video showing how a visually impaired man uses his smartphone for daily tasks such as using transportation, reading an e-book, or analyzing text from a physical object.  
The video was shot in 2012 during the Paris Web conference and is called [« Une journée accélérée en pure mobilité : une idée fixe ? » par Tanguy Lohéac](http://www.dailymotion.com/video/xw8ygi).

<iframe src="//www.dailymotion.com/embed/video/xw8ygi" allowfullscreen="" height="270" frameborder="0" width="480"></iframe>

The interface is a bit obsolete, but

## Web Fonts: serif or sans serif?

Until recently I didn't know much about the topic other than the aesthetics point of view. There are quite a few research papers about it, and one could spend an entire week switching from an opinion to the other. The topic is so debatable and debated that I couldn't find a definitive answer to my question, but the overall feeling I got is that there _might_ be some benefit in using sans serif over serif typeface in a web context, even though the magnitude may be difficult to perceive.

That being said, many experiments were done at a time when using anything other than Arial and Times New Roman was impossible, and when screens resolutions were much smaller than today. It's not like all these results are obsolete, but I feel like conducting research using more modern fonts and narrowing the devices to a specific kind could be useful. For example, with a modern desktop screen using a 20 pixels font size, which font peforms better than the other ones?

People preferences are different wether they use an e-reader, a smartphone, or a television. And too many research papers mention "the Web" as a universal support, when it's only a pipe to transport information. Since a website can be viewed on a dozen of different devices and contexts, finding the universal typeface for "the Web" doesn't make sense anymore, and sounds like looking for a unicorn.

It all depends on the user's profile and preferences, know your audience.

* [How Serif and Sans Serif Typefaces Influence Reading on Screen: An Eye Tracking Study.](https://link.springer.com/chapter/10.1007/978-3-319-40355-7_55)

  > This study aims to investigate how serif and sans serif typefaces influence reading from screen. 10 graduate students voluntarily participated in the study. The data were collected in a laboratory setting. Participants were asked to find the misspelled words in two different texts written in serif and sans serif typeface. The participants tried to find the misspelled words in the texts, during the data collection there was no time limitation. Participants’ eye movements were recorded by Tobii 1750 eye tracker device. The data were analyzed according to the accuracy and eye behavior metrics. The findings showed that participants read from sans serif typeface faster and more accurate than serif typeface. The findings suggest that participants fixated on the misspelled words more on serif typeface than sans serif typeface, in terms of the total visit duration participants spent more time on serif typeface than sans serif typeface.

* [Do serifs provide an advantage in the recognition of written words?](http://www.tandfonline.com/doi/full/10.1080/20445911.2011.546781)

  > A neglected issue in the literature on visual-word recognition is the careful examination of parameters such as font, size, or interletter/interword spacing on reading times. Here we analysed whether serifs (i.e., the small features at the end of strokes) play a role in lexical access. Traditionally, serif fonts have been considered easier to read than sans serif fonts, but prior empirical evidence is scarce and inconclusive. Here we conducted a lexical decision experiment (i.e., a word/nonword discrimination task) in which we compared words from the same family (Lucida) either with a serif font or with a sans serif font—in both a block list and a mixed list. Results showed a small, but significant advantage in response times for words written in a sans serif font. Thus, sans serif fonts should be the preferred choice for text in computer screens—as already is the case for guide signs on roads, trains, etc.

* [Changing Fonts in Education: How the Benefits Vary with Ability and Dyslexia](http://www.tandfonline.com/doi/full/10.1080/00220671.2012.736430)

  > Previous research has shown that presenting educational materials in slightly harder to read fonts than is typical engenders deeper processing. This leads to better retention and subsequent recall of information. Before this extremely simple-to-implement and cost-effective adaptation can be made routinely to educational materials, it needs to be shown to benefit all students, or at the very least not to hinder any particular group. The authors found that students across the ability spectrum demonstrate a significant improvement in retention and recall when presented with information in a disfluent font. Significantly, those students with dyslexia are also found to greatly benefit.

* [Which Are More Legible: Serif or Sans Serif Typefaces?](http://alexpoole.info/blog/which-are-more-legible-serif-or-sans-serif-typefaces/)

  This is one of the most concise and pleasant to read articles I stumbled upon. One may agree with Alex or not, it's still written in a very high quality style.

* [Fighting bad typography research](http://alexpoole.info/blog/fighting-bad-typography-research/)
* [So, What Size and Type of Font Should I Use on My Website?](http://usabilitynews.org/so-what-size-and-type-of-font-should-i-use-on-my-website/)
* [A Comparison of Popular Online Fonts: Which Size and Type is Best?](http://usabilitynews.org/a-comparison-of-popular-online-fonts-which-size-and-type-is-best/)
* [Which Fonts Do Children Prefer to Read Online?](http://usabilitynews.org/which-fonts-do-children-prefer-to-read-online/)

https://github.com/paypal/accessible-html5-video-player

https://cpu.dascritch.net/post/2016/12/14/St%C3%A9phane-Deschamps%2C-Coordinateur-accessibilit%C3%A9-et-open-source-chez-Orange
