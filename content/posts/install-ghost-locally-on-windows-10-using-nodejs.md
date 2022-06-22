---
title: Install Ghost Locally On Windows 10 Using Node.js
date: 2018-07-14 15:05:36
updated: 
type: post
tags: [ghost, windows, nodejs]
---

I'm now using Ghost to run my blog instead of WordPress, and I had a need to run a local instance on my computer to make it easy for me to port across my old WordPress theme to it.

It's actually a really simple process to install it locally on Windows 10. Really simple, no messing around with databases, no editing config files, just a download, and a few commands.

---

We need to use Node.js, so we'll start by grabbing the latest stable version from [NodeJS's website](https://nodejs.org/en/). As of writing it's `8.11.3` (the LTS version).

Once you've downloaded the `15.9 MB` file run the `.msi`, or if you like making your life harder, why double click an icon when you could "just" `msiexec /i node-v8.11.3-x64.msi`...

Follow the installation through, clicking `Next` on each page. It requires no other input than that. No need to change any of the preset defaults. It won't take long at all. Click `Finish` when done.

![2018-11-01-11_12_38-Node.js-Setup](/images/2018-11-01-11_12_38-Node.js-Setup.png)

Once it's installed, search for and open up `Node.js command prompt`.

![2018-11-01-11_14_47-Window](/images/2018-11-01-11_14_47-Window.png)

We need to install the Ghost CLI which will be our very willing helper in installing Ghost for us. So, in the Node command prompt type the following:

```
npm i -g ghost-cli@latest
```

This will install Ghost using the Node Package Manager (NPM) with the latest version of the CLI. All being well you should see an output that looks like the below:

![2018-11-01-11_19_31-Node.js-command-prompt](/images/2018-11-01-11_19_31-Node.js-command-prompt.png)

Next up we can install Ghost itself. Exciting!

Firstly, we need an empty directory to install it into. It won't install without the directory being empty. I prefer to install stuff like this on the root of the drive, so `C:\ghost` for example. Bare in mind, if you've followed this far, you'll have to change to the root using `cd C:\` as you're probably currently in `C:\Users\Username`

To create the directory either use File Explorer, or within the command prompt window type:

```
mkdir ghost
```

You can now install ghost locally, change to the directory you just created, using `cd` and simply type:

```
ghost install local
```

Boom! Simple as that!

Ghost will have installed a non-production, local development instance of itself, perfect for messing around with and working on theme development.

If it's gone to plan you'll see a final output that looks like this:

![2018-11-01-11_23_18-Node.js-command-prompt](/images/2018-11-01-11_23_18-Node.js-command-prompt.png)

You'll most likely get a a Windows Security Alert if your using Windows Defender, or something similar if using another firewall. You can allow this through.

![2018-11-01-11_22_48-Windows-Security-Alert](/images/2018-11-01-11_22_48-Windows-Security-Alert.png)

After the command has run, in the output you'll get a link to the local installation of Ghost. It'll most likely be at `http://localhost:2368` for the frontpage and `http://localhost:2368/ghost` for the administration side of things, but the port may vary.

You may have noticed that Node.js will have opened another largely blank command prompt window. Don't close this, as this is the actual running instance of Ghost. and it'll open each time you run Ghost.

Let's hop over to `http://localhost:2368` and check all is well. If it is you'll be faced with the default Ghost homepage.

![2018-11-01-11_24_25-Setup---Ghost](/images/2018-11-01-11_24_25-Setup---Ghost.png)

You can now access the below commands to start/stop/restart Ghost:

```
ghost start
ghost stop
ghost restart
```

The commands will only work if you are running the Node.js command prompt from the folder you installed Ghost too, in our case `C:\ghost`.

Now, if you're installing Ghost locally like this you may be doing it to edit themes in a slightly easier way. If that's the case you can go further and install `nodemon`. This is not a Ghost tool, but it watches your Ghost folder, and restarts Ghost when it detects a change. Making it much easier then having to constantly type `ghost restart` everytime you make a change to the theme.

To install it we need to stop Ghost by typing `ghost stop` and then we can use the Node Package Manager to install nodemon.

```
npm install -g nodemon@latest
```

![2018-11-01-11_26_40-Select-Node.js-command-prompt](/images/2018-11-01-11_26_40-Select-Node.js-command-prompt.png)

Once installed you can use nodemon to monitor your theme folder. For instance if I have a theme I'm working on within my local Ghost install, located in `C:\ghost\content\themes\new-theme` then I would type:

```
nodemon current/index.js --watch content/themes/new-theme --ext hbs,js,css
```

The image below shows what that would look like if we used the default Ghost theme `casper`:

![2018-11-01-11_29_03-Node.js-command-prompt---nodemon--current_index.js---watch-content_themes_casper](/images/2018-11-01-11_29_03-Node.js-command-prompt---nodemon--current_index.js---watch-content_themes_casper.png)

What this command is doing is telling nodemon to watch for changes to the `.hbs`, `.js`, and `.css` file types in your theme folder, and then automatically restarting Ghost when a change is detected.  
You can add other file types to that command too. For example, if you are using SASS then you may want to add `.scss` to the end of the command as well.

It'll then work just like below anytime you load a page and make a change.

![nodemon-in-action](/images/nodemon-in-action.gif)

At this stage you are good to go. You have a local development version of Ghost running, and you can do whatever you need to do before pushing your changes to your production version.
