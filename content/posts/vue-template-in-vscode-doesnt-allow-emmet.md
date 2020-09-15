---
title: Vue Template in VS Code doesn't allow Emmet
date: 2020-08-10
published: true
tags: ['vscode','html','vue','emmet']
canonical_url: false
description: "I've recently been writing in Vue a lot more, and I ran into an issue in VS Code. Vue's <template> doesn't recognize Emmet abbreviations in VS Code. It doesn't seem like such a big deal I guess, but it makes everything slower when I'm coding and is a bit of an annoyance at best. I found a fix and wanted to share in case you have the same issue."
---
![vscode emmet problem](https://dev-to-uploads.s3.amazonaws.com/i/oh9v54ix8yv3d548ss6l.png)
I've recently been writing in Vue a lot more, and I ran into an issue in VS Code. Vue's `<template>` doesn't recognize Emmet abbreviations in VS Code. It doesn't seem like such a big deal I guess, but it makes everything slower when I'm coding and is a bit of an annoyance at best. I found a fix and wanted to share in case you have the same issue.

## What is Emmet?
If you don't know [Emmet.io](https://emmet.io/) it allows you to write HTML code in short CSS-like abbreviations and expand it into UI in seconds. For example, I might type something like this:

```
#page>div.logo+ul#navigation>li*5>a{Item $}
```
##### Note: this is one of the examples from the emmet website. The brackets with a $ inside allows you to use dynamic values inside your expanded elements.

Hitting tab with Emmet installed will USUALLY give you this, unless you're using Vue:

```
<div id="page">
    <div class="logo"></div>
    <ul id="navigation">
        <li><a href="">Item 1</a></li>
        <li><a href="">Item 2</a></li>
        <li><a href="">Item 3</a></li>
        <li><a href="">Item 4</a></li>
        <li><a href="">Item 5</a></li>
    </ul>
</div>
```

I use emmet as much as I can, and it really makes life easier. I can make a mess of divs all in one line and hit tab to ensure every semantically-elegant developer hates me for all time. Sorry devs, old habits die hard. Divs are just easier sometimes to get things done when I don't need to fight with the default styles on ULs and LIs, etc. Sometimes semantics are just that, semantics. Don't @ me. #sorrynotsorry

Anyway, to get Vue to play nice with VS Code, and particularly Emmet inside the Vue `<template>` tag, you apparently can install a great Vue addon called Vetur, and then modify the emmet section of your user settings.

## Installing VS Code Addons
In case you're new to VS Code, here's how to install the Vetur addon. If you've done this before, feel free to skip this part. You'll want to continue down at the "Updating your Emmet User Settings" heading below.

##### Note: Apologies but in this case I'm using Windows to develop. Not preferred, but Mac and Linux are very similar if you're using them.

### To install Vetur:
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/8gzmpavwmfewejcjityb.png)

Next, type your search and click install. It may not be the first listing, but you want the one by Pine Wu. There are a few others that are not the right one, FYI.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/6lmdmfp8yg00p63rqcbx.png)

## Updating your Emmet User Settings

### Go To File > Preferences > Settings

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/ls7mzskmjpjul3u1jlan.png)

### Search for "Emmet: Syntax" and click the "edit settings.json" link

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/mntsptndo2kh8se7j7ln.png)

### Edit settings.json
- add the emmet.syntaxProfiles property if it doesn't exist already. 
- Be sure to add a comma if there isn't one between the last property and the new emmet block. 
- Be sure to save the settings file.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/dqofdl0sodsxzyunr336.png)

Fair warning: Your list of properties will probably look different from mine.

You may need to close VS Code, and reopen (after saving the settings file) to be sure things loaded in correctly, but now you should be able to use Emmet code expansion inside the Vue `<template>` tag. This should also work if you're writing [Gridsome](https://gridsome.org/) or [Nuxt.js](https://nuxtjs.org/), since they are also pretty much just Vue code structured differently  with some extras. 

It does seem like there may be a few edge cases related to this for some people, but this wasn't my issue. The above fix is what worked for me so I wanted to share if you have the same thing.

Thanks for reading and Happy Coding! If you want to say hello or talk tech, [hit me up on twitter](http://twitter.com/copypastepray). I'd love to meet you.

&mdash; Ryan Carter

Also posted on [dev.to](https://dev.to/copypastepray/vue-template-in-vs-code-doesn-t-allow-emmet-1kil)