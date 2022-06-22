---
title: The Power of Get-Command and Get-Help in PowerShell
date: 2018-03-17 19:48:00
updated: 
type: post
tags: [powershell, get, help]
---

There are a loads of things in life that are true, one of them is that most people never read the Terms & Conditions, and another is that they also don't bother with the instructions before doing something! However, in my experience you often miss things you could have done with knowing, and those can turn out to be things that could have made the task so much easier. Why wouldn't we want to make our jobs easier?

Sometimes my wife says I'm lazy, but I very much disagree, I'm incredibly efficient, or at least I try to be. In every corner of my life I am always trying to find ways to do it better, or quicker, and have it take less time. We recently had a heated discussion about getting a tumble dryer. Mrs Price says "we don't need one, and your just too lazy to hang up the washing!" (I reckon 10% of the clothes are mine!) but I say, "think of all the time you could spend doing something else if all you have to do is whack it in the tumble dryer!?" Some may disagree, but this is me trying to make an (in my opinion) incredibly boring process more efficient so I can do better things and that's something built into the fibre of my being - to strive to make stuff more efficient.

Why the heck am I talking about my washing? Well it's because Windows PowerShell is my tumble dryer (I just won the top 10 worst analogies of all time award), PowerShell enables me to automate what could take forever to do, or just require too many clicks. That then allows me to get back to, well, learning more about PowerShell, but, how can I make sure I'm learning about PowerShell in the right way - and is there even a right way?

Well, alongside books and videos, I tend to learn best by doing, and that is where `Get-Command` and `Get-Help` come in **super** handy.

# The Beauty of Get-Command

When your learning a new language, you need to know the vocabulary to speak it, if you go abroad you'll probably have a small phrasebook with you so you can quickly find the words you need. `Get-Command` is PowerShell's version of that vocab phrase book, and it's extremely handy when your learning, and you're not sure what cmdlet you're looking for, or if other cmdlets exist that are related to the one your currently using.

Let's see it in action.

_If you'd like to follow along, open up Windows PowerShell (on Windows 10, just right-click Start and select Windows PowerShell - no need to run as an administrator)._

## Narrow it down

In your PowerShell prompt, type `Get-Command` and brace yourself! The list could run for a while, _especially_ if you have modules for Active Directory and Exchange installed. Don't run it this way and then go scrolling to find the cmdlet you're looking for. That is *not _an efficient way to use `Get-Command`! There's a much easier way to cmdlet discovery, and that's to use wildcards (_).

Let's say you want to do something with a Service in PowerShell, but you haven't the foggiest idea where to start. First thing to do is to avoid using Google, there's no need, not at this stage. So, how do we go about finding all cmdlets to do with Services?

It's simple:

```powershell
Get-Command *service*
```

![2018-10-31-13_34_16-W10-on-HL0255---Virtual-Machine-Connection](/images/2018-10-31-13_34_16-W10-on-HL0255---Virtual-Machine-Connection.png)

Now, there's a couple of things to notice about this.

- PowerShell's cmdlet structure is \*Verb-Noun\*, and the \*verb\* and \*noun\* are \*never\* plural, they are singular. Which is why it's \`Get-Command\`, and not `Get**s**-Command` or `Get-Command**s**` (note the s), sometimes this will catch you out, so it's worth remembering if you're not finding what you're looking for.
- The two wildcards, at the start and end of the word service, should allow us to pick up anything with \*service\* in, which is what we're after.

You'll see far fewer cmdlets are returned when you hit Enter, and the selection is much more helpful. Now, that's all well and good, but you could still say, I don't know what some of these do. That's where `Get-Help` can come in handy.

# The Beauty of Get-Help

Where as `Get-Command` is great for quickly finding a cmdlet, perhaps if you have forgotten a cmdlet you already know (and know what it does), but `Get-Help` is super helpful for giving you a glimpse into what a cmdlet does in the same kind of display format as `Get-Command`, which allows you to decide which one your after.

Additionally, it is perhaps the easiest PowerShell command to use with the added benefit that it'll teach you lots.

Type in:

```powershell
Get-Help *service*
```

![2018-10-31-13_39_56-W10-on-HL0255---Virtual-Machine-Connection](/images/2018-10-31-13_39_56-W10-on-HL0255---Virtual-Machine-Connection.png)

So, we're typing in the same except we're changing the cmdlets. When you hit return notice how there's a _Synopsis_ column, with, wouldn't you know, an excerpt from the synopsis of the cmdlets help documentation!

Now we can quickly see which cmdlets we need to use to interact with Services through PowerShell! How great is that!

## Get-Help _Gets-Better_!

So we've found the cmdlet we need, and we've decided we're going to restart a service, but do we just type `Restart-Service` or do we need to add parameters, like the name of the service?

I reckon we need to run `Get-Help` against the `Restart-Service` cmdlet and see what it does! So let's do that:

```powershell
Get-Help Restart-Service
```

![2018-10-31-13_41_28-W10-on-HL0255---Virtual-Machine-Connection](/images/2018-10-31-13_41_28-W10-on-HL0255---Virtual-Machine-Connection.png)

You'll get a brief but helpful syntax, and description with some other info that should tell you all you need to know about how to use `Restart-Service`.

Even more helpful is the Remarks at the bottom, which tell you parameters you can add on to your original `Get-Help` command to get the full help documentation, and even just see some examples to copy. The latter is going to be helpful if the syntax doesn't make any sense to you yet (it's worth reading up on PowerShell syntax, but I may post something about it one day!)

Give this a quick go:

```powershell
Get-Help Restart-Service -Examples
```

![2018-10-31-13_42_06-W10-on-HL0255---Virtual-Machine-Connection](/images/2018-10-31-13_42_06-W10-on-HL0255---Virtual-Machine-Connection.png)

Superb huh? You can now see exactly how you can use `Restart-Service` to actually restart a running service and do what you originally set out to do. The beautiful part of this, is that you can obviously run this for any PowerShell cmdlet on the system your using, and if Microsoft has included help documentation, then you'll know how to use the cmdlet.

# In Conclusion

This post could go on forever, but there's much more you can do with `Get-Command` and `Get-Help` \- and here is what you should do _right now_:

1. Run `Update-Help`
2. `Get-Help Get-Command`
3. `Get-Help Get-Help`
4. Add some parameters to the above (like `-Full` and `-Examples`)

I could write about what the above cmdlets can do, and it would be a waste of my time and yours. You can get everything you need from running the above 2 commands, and that will help you truly understand how powerful both cmdlets are when your learning (and even when your already a PowerShell pro I expect - and I'm still very very far from that!)

Here's some stuff you should remember:

- **Less is more when it comes to wildcards** \- When your trying to track down a cmdlet using wildcards, `*serv*` may sometimes produce better results than `*service*`. If you're not getting any results, try deleting a few characters and see if it helps.
- **Read the Help, always** \- This is self-explanatory, but if you need to Google how to do something, you probably haven't read the help documentation on it yet, and you'll probably find the answer in there.
- **Try the examples** \- You learn by copying, so play with the examples that you get from the `-Examples` parameter.

Thanks for your time!

I hope you've enjoyed reading.
