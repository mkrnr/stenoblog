---
layout: post
title:  "AutoHotkey Hack to Reconnect Steno Machine After Sleep on Windows"
date:   2019-08-02 21:00:00 +0200
categories: georgi plover windows
author: "Martin Körner" 
---

I totally love my [Georgi](https://www.gboards.ca/product/georgi) but one small inconvenience is the fact that it doesn't automatically reconnect to Plover after putting my Windows 10 PC in sleep/hibernate.

It seems like I'm not alone with this when following the Plover Discord chats and [Tobias Schulte](https://twitter.com/tobias_schulte) even put in the effort to fix this by [adjusting Plover](https://github.com/openstenoproject/plover/pull/1054) and introducing [an auto reconnect plugin](https://github.com/tschulte/plover_auto_reconnect_machine).
Sadly, the Plover fix was marked as `post 4.0.0` and I didn't want to wait until then.
Also, running Plover from source to get this fix wasn't very practical for my setup.

Another way to fix it would be to kill Plover when going to sleep and restarting it when waking up.
Trying this, I had issues with the system tray icon that wouldn't want to disappear from the task bar so I'd end up with multiple white Plover icons on the bottom right.
Also, it would take a few seconds before Plover started after waking up which wasn't ideal.

In the end I went for an AutoHotkey script that, when executed, performs a right click on the plover tray icon, a left click on the `Reconnect machine` menu entry, and then moves the mouse to the center of the screen.
Quite the hack but it works for me.

The script looks like this and should be saved as a file with the file ending `.ahk`:

```
CoordMode, Mouse, Screen
click, right, 1790, 1070
click, 1790, 910
MouseMove, 960, 540
```

Since the coordinates such as `1790, 1070` for the Plover tray icon are based on my setup and my screen, you'd have to adjust them.
An easy way to figure out the coordinates is to use the `MouseMove` command and some guessing.

Well, first you'd need to install [AutoHotkey](https://www.autohotkey.com/) if you don't have that already.
I really enjoy this tool, especially for keybindings on my QWERTY keyboard and for [win-10-virtual-desktop-enhancer](https://github.com/sdias/win-10-virtual-desktop-enhancer) which makes the virtual desktops of Windows 10 a lot more powerful.

Also, it should be clear that this script is not happy with changing resolutions, for example when plugging off your laptop which has a different resolution than the external monitor.
I'm sure it would be possible to make the AutoHotkey script aware of this and act accordingly but I don't really need that for now and hope that the fix by Tobias will be applied to Plover soon.

Anyways, having this script is nice but we also need to trigger it when waking up from sleep/hibernate.

This can be done by adding a task in the Task Scheduler.

For this, type `Task Scheduler` into the windows search and open it.
In the `Actions` menu on the right, click `Create Task...`.

In the `General` tab, give it a name such as `reconnectPlover` and select `Configure for: Windows 10`:

![General Task Settings]({{ site.media_url }}/posts/2019-08-02-plover-reconnect-task-general.png)

In the `Triggers` tab, add a new trigger and select `Begin the task: On workstation unlock`:

![Triggers Task Settings]({{ site.media_url }}/posts/2019-08-02-plover-reconnect-task-triggers.png)

In the `Actions` tab, add an action with `New...` and select `Action: Start a program`.
For `Program/script`, browse to the AutoHotkey.exe which is usually at `C:\Program Files\AutoHotkey\AutoHotkey.exe`.
For `Add arguments`, enter the path to the AutoHotkey script from above in double quotes.
In the end, it should look somewhat like this:

![Actions Task Settings]({{ site.media_url }}/posts/2019-08-02-plover-reconnect-task-actions.png)

In the `Conditions` tab, you can deselect `Start the task only if the computer is on AC power` in case the AutoHotkey script can also handle your laptop resolution.

Confirm with `OK` and your new task should be good to go.
