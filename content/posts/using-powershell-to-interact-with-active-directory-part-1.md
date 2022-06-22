---
title: Using Powershell to Interact with Active Directory - Part 1
date: 2017-11-02 21:52:40
updated: 
type: post
tags: [active-directory, powershell]
---

In my efforts to learn PowerShell I like to force myself to use it in my day job instead of using the GUI.

I've read somewhere that nowadays anything you can do in a Microsoft GUI you can do with PowerShell, I don't believe that was always the case, don't quote me on it, but I'm taking that philosophy where I can and using it to help me learn PowerShell.

That's a philosophy I like too, I'm a big fan of Linux and always enjoy messing around in the terminal, so to be able to kind of do the same in Windows is a big plus, and sits very nicely with me especially when it gives us the ability to automate the same ol' task.

Sometimes however, it's not always convenient to _always_ default to PowerShell in this way, like when a user is standing over you as your trying to remember what you need to type in to reset their password... Just use the flippin GUI, it'll be quicker!

Whereas sometimes it's still not convenient, but makes you look cool. As one user once told me "oooh your doing The Matrix!"... not quite, but it made me smile!

A lot of what I'll be posting here is really for my own benefit, and something to look back on I suppose as my PowerShell skills improve and I can cringe at how cool I thought I was "back then", when actually all I was doing was the equivalent of `print "Hello World"` and thinking I was a big man! - oh well it may go some way to showing I did learn what I say I learnt!

So one of the things I often have to do is look up the _Description_ field of an Active Directory user, why use the GUI when we can just do this:

`Get-ADUser -Identity svettel -Properties * | Select-Object Description`

This will return whatever is in the _Description_ field of that user, handy if you keep the computer name they are assigned in this field, and you need to remote to their PC. I use it a lot for various properties.

![pspart1](/images/pspart1.jpg)

What does the `-Properties *` mean though? It's basically telling the system to return all Active Directory account properties for that user, we can then use `Select-Object` to select and display only the _Description_ property. You'd find if you didn't do that, you could still accomplish what your after, but all account properties would be returned.

![pspart1-2-1](/images/pspart1-2-1.jpg)

Something to bare in mind is that you can't really break anything with `Get` commands, I expect you probably could if you tried to "Get" a **huge** list of some really long properties across thousands of users - maybe you'd crash a server, so don't try doing that, but on a small scale `Get` isn't going to cause any issues.

When I'm not doing it in PowerShell I use _ADAC (Active Directory Administrative Center)_ a lot, it's much better then the standard _Active Directory Users & Computers_ for many reasons, one of which is it shows you the underlying PowerShell behind the GUI operations your carrying out in real-time, super-handy. One thing it's a little bit naff at is displaying lots of data though, for instance, when you want to see a list of groups a user is a member of (and vice versa), ADAC will only show 3 users at a time in the _Members_ box and you need to scroll to see others, a real pain in the neck when you want to quickly see how many, or who is in the group.

![pspart1-3](/images/pspart1-3.jpg)

_Active Directory Administrative Center, found under Administrative Tools._

![pspart1-4](/images/pspart1-4.jpg)

_As you can see, you only see 3 users at a time._

A nice quick way to accomplish this with PowerShell is with the following `Get` command, and it's slightly different depending on the point of view your taking - you'll see what I mean below.

**View Groups an AD User is a member of:**  
`Get-ADPrincipalGroupMembership -Identity svettel`

You'll then get an unsorted list returned of all the groups that, that user is a member of.

![pspart1-5](/images/pspart1-5.jpg)

**View Users who are members of an AD Group:**  
`Get-ADGroupMember -Identity Ferrari`

This will give you a list of all users within a group, as opposed to the above.

![pspart1-6-2](/images/pspart1-6-2.jpg)

If you run this, you'll notice it returns more than just usernames, things like _distinguishedName, objectGUID_ and other properties, which can "muddy the water". If you just want to see a nice alphabetically sorted list of the results, you can add the following to each command:  
`| Select-Object Name | Sort-Object Name`

So the commands would now look like this:

`Get-ADPrincipalGroupMembership -Identity svettel | Select-Object name | Sort-Object name`

`Get-ADGroupMember -Identity Ferrari | Select-Object name | Sort-Object name`

Doing this give's you an actual nice to look at list, and is really handy for quickly seeing who's in a group. You are just telling PowerShell to _select_ only the name of a user, and then _sort_ alphabetically by name. Pretty simple.

![pspart1-7](/images/pspart1-7.jpg)

![pspart1-8](/images/pspart1-8.jpg)

I think that's enough simple PowerShell for now, more to follow!
