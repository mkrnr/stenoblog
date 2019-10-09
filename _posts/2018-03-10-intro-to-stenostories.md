---
layout: post
title:  "Intro to Stenostories"
date:   2018-08-13 10:30:00 +0200
categories: stenostories
author: "Martin Körner" 
---

While browsing the [Plover subreddit](https://www.reddit.com/r/Plover/) end of last year, I found a [post by Kenneth Burchfiel](https://www.reddit.com/r/Plover/comments/757w5u/roperemembering_outlines_in_plover_more_easily_a/) about his project called ROPE – Remembering Outlines in Plover more Easily.
Struggling with finding and learning optimal strokes myself, I was super interested in his approach.
ROPE uses a program called [Anki](https://apps.ankiweb.net/) for spaced repetition learning.
Kenneth built his list with a [word frequency list by Mark Davis containing 5000 word](https://www.wordfrequency.info/) and, in addition to the spaced repetition, he added many mnemonic stories to make strokes more memorable.

To allow versioning and collaboration, I decided to port it away from the Excel-Format and onto a git repository.
Since the licensing of the original word list was not 100 percent clear, it was replaced by the [NGSL word frequency list](http://www.newgeneralservicelist.org/).
After the initial porting and publishing on GitHub, [not much happened after Nov 18, 2017](https://github.com/mkrnr/stenostories/commits/master).
I was using the list on my commute to work on a regular basis but didn't find the time to write a post about it or update the list on GitHub.

In the meanwhile, Kenneth improved the original ROPE list and recently launched [version 2.1](https://www.reddit.com/r/Plover/comments/8wzppp/rope_21_remembering_outlines_in_plover_more).
As a result, the original ROPE list by Kenneth and the one in the GitHub repo differed so much that I decided to rename my list to avoid confusion.

Here's a summary of stenostories:

* It's [hosted on GitHub](https://github.com/mkrnr/stenostories) to allow collaboration.
* The lists (currently only the NGSL one) are stored in a TSV (tab-separated values) file to allow versioning.
* There's a [.apkg file](stenostorie://github.com/mkrnr/stenostories/blob/master/stenostoried.apkg) that contains the formatting information for Anki.
* A [separate project](https://github.com/mkrnr/stenostorieshelper) contains scripts for for general maintenance.
* The [NGSL list](https://github.com/mkrnr/stenostories/blob/master/lists/ngsl.tsv) has around 5000 entries.
* It only contains strokes that come with the default plover dictionary.
* It contains plurals, conjugations, and other forms but only if they are non-trivial. For example, plurals that just add an `-S` to the root are not on the list.

And here are screenshots of an Anki flashcard from the NGSL list:

![Anki flashcard front]({{ site.media_url }}/posts/2018-08-13-anki-flashcard-any-front.png){: .center-image }


![Anki flashcard back]({{ site.media_url }}/posts/2018-08-13-anki-flashcard-any-back.png){: .center-image }

If you're interested in using stenostories, the easiest way to do so is by downloading the [deck from AnkiWeb](https://ankiweb.net/shared/info/1298398907) and import it on the Anki desktop or mobile app.
Even though the iOS app is rather expensive, the flawless synchronization between mobile and desktop makes it absolutely worth it for me.

Importing the TSV files to/from Anki is a tiny bit more work and I'll write another post about that.
In general, you first have to import the [stenostories.apkg file](https://github.com/mkrnr/stenostories/blob/master/stenostories.apkg) to get the formatting information and then importing the TSV file by applying the stenostories format.

Also, there's a [separate TSV file](https://github.com/mkrnr/stenostories/blob/master/lists/ngsl-old.tsv) for old entries that are removed from the list over time.
By importing this file, the corresponding entries in the Anki deck get marked with an `old` tag which then makes it very easy to remove them from the deck all at once.
This is important in case you want to keep your own copy of the deck with your own stories up-to-date with the GitHub version.

If you ever come to the point that you're making up your own stories which you would like to contribute for others to use, this could be done via a [pull request](https://github.com/mkrnr/stenostories/pulls) on GitHub containing the changes to the TSV file.
I'd be happy to assist you with this.

Finally, I want to again thank Kenneth for his amazing work on ROPE!
