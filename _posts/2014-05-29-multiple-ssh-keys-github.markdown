---
layout: post
title:  "Managing multiple github.com accounts with ssh keys"
date:   2014-05-29 14:10:40
categories: jekyll update
---

For various reasons I have two account with github.com. One for work and one for personal. If you find 
yourself in a similar scenario and you use ssh access to gihub then this article may provide a useful way
to organize your world.

If you haven't already done so, go ahead and [generate ssh keys] for each account on your machine. If you
have them setup already, name them something descriptive so you can tell them apart. From here on I'm going
to refer to "workuser" and "personaluser" as the two github usernames, replace them with your actual usernames
or something else meaningful.

~~~bash
~/.ssh/github.com-workuser-id_rsa
~/.ssh/github.com-personaluser-id_rsa
~~~

### Configure SSH

Now configure ssh to know how to use the correct key

~~~
vim ~/.ssh/config
~~~

Add the following

~~~
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/github.com-workuser-id_rsa

Host personaluser.github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/github.com-personaluser-id_rsa
~~~

Note in this case we're making our work account the "default" account by using "Host github.com". This means
when you copy the clone links from github It'll Just Work (tm). For your personal repos you'll need to modify
the hostname to "personaluser.github.com"

### Modify hosts for existing repos

If you have existing checked out repos for your personal account you'll need to modify the config for that repo

~~~bash
cd path/to/my-repo
vim .git/config
~~~

modify the references to github.com to be personaluser.github.com, E.G.

~~~
...
[remote "origin"]
    url = git@personaluser.github.com:jontodd/jontodd.github.io.git
    fetch = +refs/heads/*:refs/remotes/origin/*
...
~~~

Of course you can choose to make your personal account be the default or have no default by changing the Host 
configuration of your work account in your ~/.ssh/config.

### Test it

Clear your ssh context

~~~bash
ssh-add -D
~~~

Test personal account

~~~bash
$ ssh -T git@personaluser.github.com                                                
Hi personaluser! You've successfully authenticated, but GitHub does not provide shell access.
~~~

Test work account

~~~bash
$ ssh -T git@github.com                                                
Hi workuser! You've successfully authenticated, but GitHub does not provide shell access.
~~~

That's it! If you run into trouble with ssh take a look at [github's ssh help]

[generate ssh keys]: https://help.github.com/articles/generating-ssh-keys
[github's ssh help]: https://help.github.com/categories/56/articles
