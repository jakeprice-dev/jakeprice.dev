---
title: How I Manage My Files
date: 2021-12-18 22:34:22
updated: 
types: post
tags: [storage, file, directory, organisation, backup, sync, syncthing, borg, foldersync-pro]
---

Enjoy this deep dive into how I manage my files.

## Settling on a Directory Name

For a while, as silly as it sounds, I couldn't settle on a name for a directory to store all of my files. The reason it mattered to me was that I don't tend to use the default "Documents, Music, Pictures" paradigm that most operating systems provide you with. Having just a single, parent directory means I can ignore other directories and store all of my digital "stuff" in a directory that can be copied, backed up, and synced easily - without the need to specify a list of folders and filea to _ignore_ within a messy `~` (home) directory.

Structure matters to me in much of my life, so this is the sort of thing that I like to think about. I'm not the sort of person that can live with a desktop _full_ of overlapping icons. In my IT Support days I always remember being surprised by how many unorganised file organisation "schemes" I came across from individual users. Chaos was the default!

Eventually I settled on a directory name of `my` (for _my_ files) with an awareness that it's not all that different to the classic Windows-ism "My Documents" and it's certainly a name that didn't really warrant all the thought I put into it! The `my` directory stores more than just documents though, it stores everything digital that is of any importance to me.

## Structure

Below `my` I have another directory called `files`. Although I must say that's probably a wee bit redundant (mind you I originally had it "sat" alongside an `archive` directory, so there was some logic behind it).

Anyway, under `files` sit four _core_ directories which generally cover all the file types I have or use. These _never_ change, and nothing get's added to the core directories (so far at least).

Here's what the overall structure looks like:

```sh
$ tree -L 2 my/
my
└── files
    ├── code
    ├── documents
    ├── inbox
    └── media
```

### Core Directories

There's no special structure underneath each core directory apart from in the `media` directory, as detailed in a moment.

- `code` stores all of my code, scripts and other projects. The vast majority is version controlled with Git, and some of it  is also on GitHub. The stuff that isn't on GitHub is just not up to the kind of standard I want to make public (we all have at least one disaster of a cupboard or drawer right?)
- `documents` has everything that isn't code or media, so finances, my CV, blog posts, my personal log, graphic design stuff, filing, private keys and more.
- `inbox` acts as a holding directory which I use to throw files in that I don't want to think about organising yet. The idea is I should regularly go through and move these files to a permanent place, but that doesn't really happen, so some stuff just sits there for ages.
- `media` acts as a parent directory which contains sub-directories based on the type of media contained within. You can see this below.

```sh
$ tree -L 1 my/files/media/
my/files/media/
├── apps
├── audio
├── ebooks
├── games
├── photos
└── pictures
```

## Infrastructure

Everything resides on my primary home server `host-01` which is a 4th Gen Intel i5 HP EliteDesk PC that I was allowed to take home from one of my previous jobs.

### Storage

In terms of storage I have two main disks.

- 460 GB Samsung SSD which serves up the files.
- 1 TB Western Digital Blue Hard Drive for local back ups of the files.

These drives are mounted into the below directories on `host-01`.

- /mnt/data-ssd-01
- /mnt/archive-hdd-01

It should be noted that I self-host a lot on `host-01` (VM's and over 30 containers) and it runs Debian 11.

#### Storage Capacity

In the grand scheme of things, I'm not storing all that much data, and I'm certainly no data hoarder (yet)... As of writing I'm storing a pretty manageable 111 GB. Unsurprisingly (to me at least) 94 GB of that is in the `media` directory with 72 GB of that being my photos directory - the vast majority of which have been taken in the last 2 years since having our first kid!

Here's a breakdown of the storage across the core directories (in GB).

```sh
$ du -h --max-depth=1 my/files/ | sort -$
2.1G    my/files/inbox
4.6G    my/files/code
10G     my/files/documents
94G     my/files/media
111G    my/files/
```

## Backups

`my` is currently backed up to two places.

1. A cron job runs a Borg Backup script each night at 3am. This backs up to my 1TB `/mnt/archive-hdd-01` on my home server.

```sh
#Ansible: Backup fileshare to Borg repository
0 3 * * * /usr/bin/bash /mnt/data-ssd-01/my/files/code/ppn/shared/scripts/borg_backup_my.sh
```

2. I also run a manual rsync backup to 1TB External Hard Drive. I have a reminder to do this each month, as it's deliberately not connected usually.

I am _acutely_ aware that I'm ignoring best practices regarding backing up _offsite_.

I do have a Borg Backup account with rsync.net that I really do need to get setup asap, but when you have two kids time is limited!

## Access

### Samba

I run Samba directly on `host-01` which serves up the `my` folder on my LAN. It's particularly handy to have a way to quickly access my files (with `smb://`...), especially when I'm initially setting up a device after a rebuild (which I do fairly often).

### Laptop

I run Fedora on my laptop, and generally do everything on it. Having kids it's super handy not being chained to my desktop PC. Gone are the days when I could spend hours at the weekend shut away in my office tinkering! Although that urge hasn't gone, so a laptop is great - and it allows me to still be present with my family, but also do all the other computer stuff I'm passionate about too. In my case, my laptop really is an extension of, well, my lap - thankfully I have a wife who supports all my "techy" stuff as she puts it.

So, on my laptop I need to have reliable access to `my`, and over the years I have tried a few different tools.

#### Syncthing

[Syncthing](https://syncthing.net/) is an open source syncing tool which I've tried to use a lot of over the last few years. It's an often recommended tool for use cases like mine, but unfortunately I've _never_ got on with it. Everytime I have used it I have ran into problems. For me, it's initial sync is dial-up slow even when I verify it's all happening on my LAN and not over a relay. It obviously works for lots of people, and I know that some people are syncing hundreds of gigabytes with it, but alas, I've never gotten it to work well and every time I try it just frustrates me.

#### Samba Mount

One of the other things I have tried is to cut out the "middle-man" and do away with syncing completely by mounting `my` as served up by Samba. This was very much my ideal solution, especially on my LAN, because I didn't generally notice any lag in file operations (read, write etc) which is important. However, I did notice a number of things that eventually became enough of a frustration that I abandoned the mount solution.

1. Build operations can be a lot slower over the network. One example of this is with local development of big [Hugo](https://gohugo.io/) static sites. I use Hugo for my personal log (`my/files/documents/log`, and I have thousands of files in it. Running the command `hugo server` (which builds the site and serves it up on localhost) takes a ridiculous amount of time - significantly longer then if the files are physically on my laptop.
2. I generally use Vim for all my text editing/scripting, and I'm also a serial (multiple times a minute)`:w`'er (I hate autosave, and don't trust configuration pages without a save button!!). Saving as regularly as I do when I'm editing in Vim, I quickly discovered an issue - for whatever reason, Vim would often tell me that the file had changed - which became really annoying. Having looked into it [here](https://vi.stackexchange.com/questions/16617/suppress-bypass-file-has-changed-errors-when-editing-cifs-samba-files) the recommended solution of adding `actimeo=0` to my CIFS mount in `/etc/fstab` worked, but resulted in a catastrophic performance degradation!

So, mounting `my` wasn't a solution in the end either. I was and still am surprised as how, at least in my experience, syncing local files is actually harder than you'd imagine - at least in comparison to downloading a client for Google Drive or OneDrive on Windows.

#### Unison

I lived with the mount solution for a long time, before starting to think about a more manual solution. I remember hearing in an interview on [Linux Unplugged](https://linuxunplugged.com/) how the interviewee used rsync for manually syncing his files and just triggered it when he wanted to.

I've used rsync before, not for anything overly complex, but quickly found out that it wouldn't work the way I wanted it, as the Unison project puts it:

> Rsync is a mirroring tool; Unison is a synchronizer. That is, rsync needs to be told "this replica contains the true versions of all the files; please make the other replica look exactly the same." Unison is capable of recognizing updates in both replicas and deciding which way they should be propagated. 
>
> -- [Unison FAQ](https://alliance.seas.upenn.edu/~bcpierce/wiki/index.php?n=Main.UnisonFAQGeneral)

I discovered that "quote" after I knew anything about Unison though, so eventually worked this out myself when rsync wasn't doing what I was expecting it to!

I run Unison in a Docker container I've built, that runs via cron every 5 minutes. I can specify exactly what I want to sync in my Unison profile file, which you can see an example of below. On my laptop that's generally everything in `my` apart from some particular problem files (files that are often in use etc) or files that get built on demand (Hugo static sites etc).

```ini
# Sync roots
root=/home/jprice/my
root=ssh://<username>@<host>//mnt/data-ssd-01/my

# Sync options:
sshargs=-oIdentityFile=~/.ssh/ppn-int-ho-hl-hs-host-01

# Sync paths:
path=files/code
path=files/documents
path=files/inbox
path=files/media

# Log options:
log=true
logfile=/var/log/unison/unison_sync_elitebook.log

# Ignore paths:
ignore = Name .DS_Store
ignore = Name audio/podcasts/library
ignore = Name bible/public
ignore = Name log/public
ignore = Name ppn/services/containers/compose/speedtest-tracker/config
ignore = Name ppn/services/containers/compose/uptime-kuma/uptime-kuma
ignore = Name ppn/services/containers/compose/prometheus/prometheus/data
ignore = Name ppn/services/containers/compose/wallabag/wallabag/data/site-credentials-secret-key.txt
ignore = Name photos/_files/cache
```

If I want to manually run it (and I often do), perhaps because I need a change on another device asap (like my phone) I have an alias set in `.bashrc` to run the same Docker command I am running at 15 minute intervals via cron. That means I can just type `my-sync` into my terminal and include any extra parameters for Unison I want (`--batch`) and the container will spin up and sync on-demand.

### Android

#### FolderSync Pro

I've tried just about all of the solutions above on Android too with varying levels of success. I can always connect to my VPN to grab a file if I need to, but I want to sync some of what is in `my` regardless, especially in case of no connection at all.

As mentioned a bit earlier, on my laptop I originally tried Syncthing, and when I did that I had it syncing between `host-01`, my laptop and my Android phone. 

Regardless of my thoughts on Syncthing, the beauty of Syncthing _on Android_ is how well it integrates with the filesystem. You simply create and link a folder or folders in the phones "home" (`/sdcard`) directory. So unlike as can happen with some apps, your files are synced to the device as proper files, in proper directories and aren't hidden away under some obscure path. You can have everything at `/sdcard/my` sitting alongside Android's default directories (Download, Music, Pictures etc), so it's very easy to use your files just as you do on a laptop.

One of the things I didn't mention earlier as to why I abandoned Syncthing was that syncs were mostly _instant_. (I can't remember if you can turn that functionality off or not?) Regardless, if Syncthing detected a change it would sync it - right away. In theory, that's nice functionality to have, but in practice I found it to be overkill for my use-case and unnecessary. I just don't need instant sync. In fact I actively don't want it, and sometimes even want to be able to temporarily deactivate all syncs, so I can extend my battery life.

The solution to these issues came in the form of an excellent app called FolderSync Pro. The great thing about it, is you can download the APK from the developer (Tacit Systems) directly and there is no dependency on having Google Play Services installed. It's absolutely rock solid, and I've used it for over 2 years now with literally no issues. I sync every hour and it usually uses around 1 to 1.5%. 

## Conclusion

So, in summary, that's about it, I hope you've enjoyed reading.

