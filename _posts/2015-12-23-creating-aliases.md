---
layout: post
title:  "Creating Aliases"
date:   2015-12-23 21:28:15 +0700
categories: [JavaScript]
---

## Creating Aliases

There are two approaches to getting awesome at the terminal. You can learn all the commands, or you can just make your own commands that are shortcuts to those commands. 

I would say learn the basic or most used commands and then do shortcuts for all the rest. The more productive you are as a developer the better. In that note, you can create your own shortcuts or you can just install aliases other people have made. Be careful when you do decide to do it. There are many dotfile installations that will break your system. So make sure that you are prepared for that. A dot file that is well tested is the following:
https://github.com/vjefri/dotfiles-1

![](http://i66.tinypic.com/jugwb9.png)
It is super cool when you have this type of control out of your terminal. You can just do `l` and it will list the files and folder in a long list. 

If I want to edit my aliases I just do `ealias` and I am ready to roll. I created that command. It does not come with the above installation. However, some really cool commands do come with Mathias's dotfiles. 

In order to edit the alias file you will have to run the following command on the terminal `open .aliases`, which basically means that we want the hidden file .aliases to open. You can also run `la` to list all files including hidden files. 

Here is a cool list of shortcuts that will appear when you run that command. 

{% gist 9b90a49a98900de41223256b513ef327 %}

You can save time by doing this. I will caution to only use it once you understand the commands and have used them a few times. Because if someone asks you how add to upstream via git you will `prum` when really you want say `git remote add upstream`. 

Happy hacking. 