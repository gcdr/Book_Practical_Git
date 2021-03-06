## Is Git a Single point of failure for TeamMentor?

Danny is getting into Git and just asked-me this:  

_"is it possible for Git to be a single point of failure for TM? If Git went down or offline, wouldn't that be a problem?"_  

The short answer is **"NO, in fact Git is a distributed point of success for TM"**  

Let's start with the differences between **Git** and **_GitHub_**.

Think of **Git** as a **_'file-based database of multiple versions of a particular file, with one version shown in the file system',_** i.e. 'Git' is the **.git** folder and a checkout version of the files (in the file system)

Think of **GitHub** as a **'web based location to store and share the .git folder'**  

This means that a **Git** repository doesn't go '_down or offline'_. A Git repository is just a **.git** folder, and if you wanted to remove **Git **from a particular folder/repository, you could just delete that .git** folder (and you would be left with the latest '_checked-out version of the files'_)

In terms of **GitHub** going down, there are two main scenarios:

**1) _GitHub_ loses the _.git_ folders that it hosts** (i.e. it loses the git repositories) - this would be a pain, but as long as there is one clone of those repositories, there shouldn't be much/anything lost. This is why I say that '**_Git has distributed points of success'_**, basically, every clone or fork that exists, is in effect a backup of the code (there are a couple things like remote information that is not cloned, but those are minor)

**2) GitHub.com is down** - the impact will depend on how long this happens, at the moment we do use GitHub as a central way to distribute and publish source code between TM devs and servers, so if GitHub is down (more specifically, GitHub's Git hosting service, not the GitHub.com website), then we can't push the commits made (note that the devs can still work on the local git clones, and TeamMentor users can still edit Git based Libraries). Even in the case where GitHub is down for a significant time, there are easy solutions to implement (specially when you compare with the fact that if GMail, Google or Twitter goes down, there is nothing we can't do).  Part of the power of Git is that all commits are tied to its Hash, which means that while GitHub is down, we could host our own git server (see [here how I did it using apache](http://blog.diniscruz.com/2013/03/setting-up-apache-httpd-based-git.html)) or push commits directly to Azure (which can also act as a Git Server). Then once GitHub is back online all we need to do is to push the commits to it.

The other scenario that could happen on GitHub is that those repositories are maliciously manipulated (lets say by an internal attack that is able to add extra commits). But since of the key advantages of **_Git_** is that it is a DRCS ([Distributed Revision Control System](http://en.wikipedia.org/wiki/Distributed_revision_control)) and the entire version history is present on all clones/forks, in practice, the next 'real' commit would fail, which should raise the alarm (i.e. that developer would need to do a git pull before it could push the code)

The way I look at **_Git_** is that it creates a '_**virtual file system, fully hashed and with version control'**_, which you can read more about in the post: [Linus gift to the world will be Git not Linux (and what about an OS built on top of an hash-driven file system?)](http://www.blogger.com/blog.diniscruz.com/2013/04/linus-gift-to-world-will-be-git-not.html)
