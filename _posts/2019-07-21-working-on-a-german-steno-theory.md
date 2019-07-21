---
layout: post
title:  "Working on a German Steno Theory"
date:   2019-07-21 17:45:00 +0200
categories: regenpfeifer
author: "Martin Körner" 
---

Last days I finally found some time to work on a long-term goal of mine: A German steno theory similar to the default English steno theory that is provided with [Plover](https://github.com/openstenoproject/plover).
It seems like there already is a [theory out there](http://www.zav.cz/german/compkomasch.htm) but it's not publicly available and the keyboard layout is painfully different from the standard English one:

![Proprietary German Layout]({{ site.media_url }}/posts/2019-07-21-proprietary-german-layout.png)

While the English layout probably isn't optimal for the German language, I have a feeling that it's not too far off and I definitely would prefer to have similar layouts when switching between German and English.

Thereby, I decided to keep the English layout except for one key:
The `-Z` is replaced by an `-N` as a suffix `-en` which is used quite a lot in German:

![Regenpfeifer Layout]({{ site.media_url }}/posts/2019-07-21-regenpfeifer-layout.png)

Also most key combinations to form other letters are the same.
By the way: The layout images were creating by manipulating the HTML on Ted's [Art of Chording](https://www.artofchording.com/) website and taking screenshots...

Plover makes it super easy to add a new theory and the above layout can be found on [GitHub](https://github.com/mkrnr/plover_german_regenpfeifer).
For now, it can be installed manually with the following command:

```
.\plover_console.exe -s plover_plugins install <path-to-regenpfeifer-git-repo>
```

At some point you should also find it in the Plover Plugin Manager as `plover_german_regenpfeifer` but I'd like to add some orthography rules before uploading the first version.
And yeah, I want to call this theory [Regenpfeifer](https://de.wikipedia.org/wiki/Regenpfeifer) which is German for plover and directly translates to rain whistler :-)

Creating the Plover plugin for the Regenpfeifer system was a nice first step but the way more challenging task is to build a dictionary.

First, I needed a good list of German words, preferably sorted by frequency.
Also, the Nouns like `Auto` and `Baum` on that list have to be capitalized which is not the case for some lists.
Last but not least, the list should have a reasonable license.
The best one I found was the [DeReWo](http://www.ids-mannheim.de/derewo) list by IDS Mannheim.
Using [pattern.de](https://www.clips.uantwerpen.be/pages/pattern-de) by the CLiPS Research Center of the University of Antwerp, I generated all the different word forms such as plurals and conjugations.
The resulting list is on [GitHub](https://github.com/mkrnr/wortformliste) and has the same license as the original DeReWo list.
This list, however, is work in progress since the automated word form generation is not perfect.
It would make sense to go over the list and remove words that don't exist.

A central part when building new strokes for words is to figure out which vowel is emphasized and for this I wrote a simple [word emphasizer](https://github.com/mkrnr/regenpfeifer/blob/master/regenpfeifer/word_emphasizer.py) based on rules and heuristics that I collected online.

My first idea was to build a neural network based on the Plover dictionary and run it on my word list but sadly I couldn't produce any usable results.

Thereby I went for a simple [pattern-matching approach](https://github.com/mkrnr/regenpfeifer/blob/master/regenpfeifer/word_pattern_matcher.py) to build my dictionary and the patterns which are separated in left consonants, vowels, and right consonants can be found [here](https://github.com/mkrnr/regenpfeifer/tree/master/regenpfeifer/assets/patterns).
After applying this rather simple pattern matching, the results need to be [validated](https://github.com/mkrnr/regenpfeifer/blob/master/regenpfeifer/stroke_validator.py) to see if they fit the steno order.

The current result of this approach can be found in the [GitHub repo of the Regenpfeifer plover plugin](https://github.com/mkrnr/plover_german_regenpfeifer/blob/master/plover_german_regenpfeifer/dictionaries/main.json).

Some examples that turned out quite reasonable:
```
"AUFPBLN": "aufnehmen"
"EFPT/EFTN": "echtesten"
"ER/TPRAOEUR/EPBD": "erfrierend"
"HAOEULT/EFT": "hieltest"
"KOERPB": "Könner"
"PWHROU/EPBD/EPL": "blühendem"
"SAOEUBN": "sieben"
"TKPWE/HROEUT/ET": "geläutet"
```

These have some room for improvement:
```
"AUFT/EL/EPB": "ausstellen"
"ER/AELT": "erhält"
"HERS/EPB": "hersehen"
"KERPBT/EPLN": "Kernthemen"
"OFT/ERPB/-FT": "Osternest"
"OUB/ERS/EPBD/EPB": "übersenden"
```

Currently, the main issue is a reasonable separation when building a word from multiple strokes.
And of course there are many words that don't have any matches.

Thereby, the next steps will be to extend the patterns and to figure out a way to deal with those famous long German words such as Donaudampfschiffahrtsgesellschaftskapitän.
Well, I guess there should be a brief for that one.
But such cases aside, the best would be to have a command on Plover which allows to concatenate the last X words which probably requires a new plugin.
Other than that, briefs for the most frequent words similar to the `-T` for `the` in the Plover theory need to be built as well as finger-spelling and so on.
Last but not least, the theory should be documented so that it's possible to learn it without going through the [pattern files](https://github.com/mkrnr/regenpfeifer/tree/master/regenpfeifer/assets/patterns) to figure out the logic.

As you can see, there is still quite some work to be done before Regenpfeifer is actually usable.
If you're interested in getting your hands dirty, just let me know!

