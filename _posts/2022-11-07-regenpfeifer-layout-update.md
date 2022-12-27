---
layout: post
title:  "Regenpfeifer Layout Update"
date:   2022-11-07 20:15:00 +0100
categories: regenpfeifer german theory
author: "Martin Körner" 
---

After focussing on fingerspelling and the English theory for the last years, I recently revisited the German steno theory Regenpfeifer that I described in a [previous blog post]({% post_url 2019-07-21-working-on-a-german-steno-theory %}) and which can be installed as the plugin [plover-regenpfeifer](https://github.com/mkrnr/plover_regenpfeifer) via the Plover Plugins Manager.

With version 1.0.0 that was released today, the biggest change is to the layout.
In the original layout that I described in a, the only change was to replace `-Z` with `-N` since a lot of German words end with `en`.
After using the layout for some time, it doesn't seem worth it for me to deviate from the English layout and it's somewhat strange to have two different ways to write `n` on the right hand side.
Also, even though `-en` is a very common ending, there are many more and I prefer to handle them all the same.
Thereby, version 1.0.0 again uses `-Z`.

However, this version introduces a remapping for the left hand side.
As it turns out, many German words or syllables start with `z` and I really don't enjoy writing `z` with `S*`.
Thereby, the top `S-` is remapped to `Z-`.
This might become a problem for people with professional steno machines where there's only one `S-` key but I would assume that pretty much anyone interested in German uses a hobbyist steno machine.
As a result, this is the new layout for Regenpfeifer version 1.0.0:

![Regenpfeifer 1.0.0 Layout]({{ site.media_url }}/posts/2022-11-07-regenpfeifer-1-0-0-layout.png)

Of course I also regenerated the included dictionary.
There's still a lot of room for improvement and my goal is to further improve the automatically generated translations and to work on sensible briefs for the most common words.
Feel free to reach out if you want to collaborate on this!

Also, in order to stay consistent with the English layout, there's now a plugin called [Plover Mod-Z](https://github.com/mkrnr/plover_mod_z) which does the same remapping but for the English Stenotype theory that is included in Plover.
Since this just provides a new key that is not used in the English theory, all existing English dictionaries still work.
I mainly use it to type the letter `z` when fingerspelling but it might become more useful in the future.
This plugin can also be found as `plover-mod-z` via the Plover Plugins Manager.

As far as I know, nobody currently uses Regenpfeifer productively but reach out to me if that assumption is wrong and the layout change causes issues for you.

There's now a [German channel](https://discord.com/channels/136953735426473984/1034562627017388142) on the official Plover discord channel and I'm happy to discuss Regenpfeifer there.
