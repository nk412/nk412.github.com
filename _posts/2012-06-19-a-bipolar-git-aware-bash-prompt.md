---
layout: post
title: "A bipolar git aware bash prompt"
description: "A short post describing my bash prompt"
category: articles
tags: [bash, customization]
image:
  feature: so-simple-sample-image-1.jpg
comments: true  
---

What better to track the return code your scripts than have a always-on colored smiley on your bash prompt?

<figure>
	<center><img src="/images/bash_prompt/prompt.png">
	<figcaption>:)</figcaption>
	</center>
</figure>

The smiley function simply catches the exit code depending on which it returns a happy or a sad face. Catching the exit code on the very first line allows the status of the very last function to flow through, which is exactly what we need.

{% highlight bash %}
smiley(){
	local exit_code=$?
	local happy_face=":)"
	local unhappy_face=":("
	if [ ${exit_code} -eq 0 ]; then
		echo -e "\e[1;32m ${happy_face}\e[0m";
	else
		echo -e "\e[1;31m ${unhappy_face}\e[0m";
	fi;
	}
{% endhighlight %}

Since I'm working quite often with `git`, I thought it would be a neat addition to have the current working branch on the prompt. My initial naive implementation used `git status`, along with some grep and awk magic to get the current branch, but I very quickly found out that this can get very expensive especially when navigating through a repository with a lot of modified or staged files. Thanks to a quick search that led me to a post on stackoverflow, this function quickly gets the current branch without worrying about directory states. Should it fail ( or not find any valid git repository ), it returns nothing. 

{% highlight bash %}
gitbranch(){
	local br_name=$(git rev-parse \
		--abbrev-ref HEAD \
		2> /dev/null )
	if [ $? -eq 0 ]; then
     		if [ ! "$br_name" = "" ]; then
        		echo -e "\e[1;91m[$br_name]\e[0m";
     		fi
	fi
	}
{% endhighlight %}

Bringing them both together in a two-line prompt is done by the following line in `~/.bashrc`. The first line has the hostname, the status smiley, git branch and the current working path, and the next line gives me all the room I need to type my commands.

{% highlight bash %}
PS1="\h\$(smiley) \$(gitbranch) \e[30;1m\w\e[0m\n\$ "
{% endhighlight %}