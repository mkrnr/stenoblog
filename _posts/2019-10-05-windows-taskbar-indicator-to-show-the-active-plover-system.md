---
layout: post
title:  "Windows 10 Taskbar Language Indicator to Show the Active Plover System"
date:   2019-10-05 22:00:00 +0200
categories: plover windows multilingual
author: "Martin Körner" 
---

For people that use more than one steno system in Plover, for example the English Plover system as well as [a German one](https://stenoblog.com/working-on-a-german-steno-theory/), an issue is knowing which system is currently active.
Windows 10 already has an indicator for the active input method included in the taskbar (ENG/DEU/...) and here's how this indicator can be updated when switching between Plover systems.

First, you need to add display languages to Windows that correspond to the languages of your Plover theories.
For me that's English and German:

![Actions Task Settings]({{ site.media_url }}/posts/2019-10-05-windows-display-language.png)

I also changed the keyboard layout for German to QWERTY so that the keyboard layout doesn't change when switching between languages.

Next, you need to add hot keys to switch to the different input languages.
It seems like the way to get to those settings changes every few months so have a look [on superuser.com](https://superuser.com/questions/958901/set-shortcuts-to-change-keyboard-layout-in-windows-10) to see how to get to the following screen:

![Actions Task Settings]({{ site.media_url }}/posts/2019-10-05-hot-keys-for-input-languages.png)

As you can see, I added the strangest key sequences possible since they won't be used directly but added to Plover dictionary entries.
Interestingly, after adding those shortcuts I wasn't able to actually use them right away which seems like a Windows bug.
What helped in my case was changing the order of the two languages in the Preferred languages settings (see first picture).
Restarting might also help but hopefully you don't have such problems.

Anyways, after you got those shortcuts working, they just need to be added to the strokes that you use for switching between the systems:

```
"EPBG": "{PLOVER:SWITCH_SYSTEM:English Stenotype}{#alt(shift(8))}",
"TKPWER": "{PLOVER:SWITCH_SYSTEM:Regenpfeifer}{#alt(shift(9))}",
```

The functionality to switch between Plovers systems requires the [plover-system-switcher](https://github.com/nsmarkop/plover_system_switcher) to be installed which can be easily done via the Plover Plugin Manager.

Now the language indicator in the taskbar should update when using the strokes to switch between Plover systems.
As always, let me know if you have any issues.

