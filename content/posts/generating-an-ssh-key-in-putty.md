---
title: Generating An SSH Key In PuTTY
date: 2018-07-10 20:40:00
updated: 
type: post
tags: [putty, ssh, private-key]
---

I'm using PuTTY a lot more at the moment, because I've recently switched my blog over to a VPS, so I'm regularly using SSH to connect to it. I'll be posting a post about that move soon, but thought I'd take the time to document how to go about generating an encryption key in PuTTY that you can then use for your encryption needs.

If you haven't already, go and download [PuTTY](https://putty.org/).

Once you've installed it with the default options, search for and open _PuTTYgen_.

![2018-10-31-08_58_54-Window](/images/2018-10-31-08_58_54-Window.png)

The following process to generate your key couldn't be simpler, and is almost fun!

Once _PuTTY Key Generator_ is open, leave the `RSA` radio button selected, and change the `Number of bits in a generated key:` to `4096` for that added security.

It's then as simple as pressing `Generate`, and doing some wonderfully creative mouse movements to generate some randomness for your key (make sure you add a funny soundtrack).

![2018-10-31-09_00_54-PuTTY-Key-Generator](/images/2018-10-31-09_00_54-PuTTY-Key-Generator.png)

Hey Presto! You'll then see your public key, which you can use right away for whatever purpose you wish! It'll look something like this:

```shell
ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAgEAgkoIMYPNN0WOUPRRM2oofVtslCRzCYp0WHcM2hqnhBjEelV+6EA218rlyopzABv6GW3BrD0smGF5+4Jjdu9xQuXjfor9nLOMl9EnnnNALXCIxzKIefHG3UPsSMTe/p2CzvfC/VSfzNAvjV4YQHaywrxFbc85mYy+fMEU61sFr3kXnqQAe+Y78S3BJaYzUMVbq0cDP/k3PsrN5kQCCiSqoPMfYS+MZEd56/kqihzjN+/MomJ9aRgNwp0MJ2Oq+FEgzw+7u71UUBkc6IYItHXbHusc4eSVc6MlutwP0izYnfnlGeAS3gaxjbltKlbZJkDq4H0JCVlCufW1XW+5GXDoNwTTc9s6XbbsuWUEIr9Kmm/47Bl9Ahq/O2sVhZKeB5YHtUWGr0iWolONuVSzHAUM3+8CcplNkWZHpRlnA9jJ9beco7IYRCJcs1mModGjfpK+C6YtfL3BtmGfA/tffx/9AbZeV2apT0t9DPCagAj/yjsNS96+L9eKR7vQPCnd1JWWLwo5z25rsVva+ciJnqL4YffiuehSEdqeYv37bHI0++28ne6jtlU++2FI5fAlCoKMYWCznrgjTeb9+ZUdMi0Jf11kXxIY3mAp4zOJdo8Kb2aWB9wKNgbVMMbXkcTJcKonwUcGFa8LoepJKoXXc+dhc8KamrW22JVUgSPRO1zLn7U= rsa-key-20180710
```

I tend to replace the default `Key comment` field for my own sanity, and I like to add a very long `Key passphrase` for even more security.

![2018-10-31-09_02_11-PuTTY-Key-Generator](/images/2018-10-31-09_02_11-PuTTY-Key-Generator.png)

Make sure you save your public and private key's by clicking `Save public key` and `Save private key`. Ensure you save them somewhere only you can access, especially the private key.

Simple as that!
