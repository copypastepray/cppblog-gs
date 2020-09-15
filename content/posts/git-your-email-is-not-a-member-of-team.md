---
title: Your Git Email is not a member of team
date: 2020-08-04
published: true
tags: ['git','commandline','gitlab','config']
canonical_url: false
description: "Have you ever seen this kind of message when trying to push code to gitlab or github? remote: GitLab: Author 'your@email.com' is not a member of team"
---
![Your Email is not a member of team](https://dev-to-uploads.s3.amazonaws.com/i/xjgpq8c6wham4veuau04.png)
Have you ever seen this kind of message when trying to push code to gitlab (or possibly github, not sure)?

## The output
```
remote: GitLab: Author 'your@email.com' is not a member of team
! [remote rejected] TCKT-1234 -> TCKT-1234 (pre-received hook declined)
error: failed to push some refs to 'git@gitlab.com/reponame'
```

Only I never added my personal git email ID to this machine, at least not that I remember. Look it's been "a year", okay? Too much going on. So how did this happen? Better than that, how do you fix it? Quick! I was supposed to push this an hour ago and things are  broken. Ahhhh! I hate it when I have the dumb.

If you have the same problem, I know how you feel. I had the same problem too. I will likely have it again at some point, who knows?

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/cwib7oy0fxj5kn2pziys.jpg)

## What's the issue?

The issue is that another git ID got onto my computer somehow. Maybe I was exploring and trying out a new technology, signed into it with my personal git account, I backed out, or I fiddled with my settings for another project. Whatever the case, the damage was already done. To be honest, I don't even remember. #2020

## Things I tried:

First I thought, okay, well, maybe I got the wrong ID in my config. I'll just reset it. So I did.

### Global Git Config Settings:

##### In terminal:
```
git config --global user.name "John Doe"
git config --global user.email "john@doe.org"
```

that didn't work, so I tried to do locally.

### Local (this repo only) Git Config Settings:

##### In terminal:
```
git config --local user.name "John Doe"
git config --local user.email "john@doe.org"
```

This MUST fix it right? Wrong author, so I reset the author. Makes sense? I tried to push again, same issue. Why? It turns out the latest commit was fine, but not the _second to last commit_ I made. That one was a mistake. Clearly.

So what to do? Git log held the answer. Seems like I knew this at one point but hadn't needed it in a while so I forget how helpful it is. Log is a super useful command.

## How to fix it:

# 1. Check git log to see your last commits

##### In terminal:
```
git log
```

and I got a print out of all my recent commits. Screenshot redacted to protect client information security.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/gp9bef34mnkps7dy61dl.png)

# 2. Copy the commit ID

The next step is to copy the commit ID from the one you want to change. The one with the wrong email on it. 

# 3. git rebase
Then you want to run this to start the edit:

##### In terminal:
```
git rebase -i 975479bb630b8495ac44d8a95c4e056c989b5a04
```
Where your commit ID is 975479bb630b8495ac44d8a95c4e056c989b5a04.

You should see it open your default text editor and give you a line with pick at the beginning.
 
##### In Nano/Vim/text editor: 
```
pick 1a2b3c commit message here
```

Change the "pick" to "edit" and be sure not to delete the space after edit. It should read: 

##### In Nano/Vim/text editor: 
```
edit 1a2b3c commit message here
```

where 1a2b3c is the shorter version of the commit ID (it is auto added for you, don't need to add it yourself)

# 4. Save the File. 

Now you're in "edit" mode for this commit.

# 5. Update the author info with this:

##### In Terminal:
```
git commit --amend --author="Your Name <correctemail@company.com>"
```

If that goes well, then you continue the rebase with this:

##### In Terminal:
```
git rebase --continue
```

If it doesn't go well, I would google the error that you get and see if you can find more info on it. Usually I learn more this way than any other.

Once you solve any issues, you should see something like this: 

##### In Terminal:
```
Successfully rebased and updated refs/heads/develop.
```

This is how you know things worked with the rebase. Now you can push your branch or merge or whatever you were trying to do before.

I did see a few good tutorials out there, but none that had the whole process, so I tried to piece this together from a few of them.

### Warning: 
Please be careful with rebasing. You normally shouldn't need to rebase much, and if you leave off the commit id you can end up rewriting the repo's history which will cause more issues. to learn more about what a rebase is and does, check out [Atlassian's very good rebase article](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase) with pictures!

I'm a long time developer, but I'm learning new stuff every day, which is what I find most attractive about programming. 

Let me know what you think of my first article and how you think I might improve it. Thanks for your feedback.
