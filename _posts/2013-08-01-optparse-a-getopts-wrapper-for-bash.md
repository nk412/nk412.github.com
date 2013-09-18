---
layout: post
title: "Optparse: A getopts wrapper for bash"
description: "Because getopts is a lot of line noise"
category: articles
tags: [bash, projects]
image:
  feature: so-simple-sample-image-3.jpg
comments: true  
---

If you've ever used bash, you know how much of a hassle it can be to get proper argument parsing with or without using `getopts`. Once you do however get it to work, you soon realize that it's just boiler plate code that you can copy and paste to other scripts. Enter, `optparse`.

I wrote this wrapper to provide a clean and easy way to parse arguments to your bash scripts. It lets you define short and long option names, handle flag variables, and set default values for optional arguments, and also automatically build a usage description, all while aiming to be as minimal as possible: *One line per argument definition*.

##Usage

###1. Define your arguments

Each argument to the script is defined with `optparse.define`, which specifies the option names, a short description, the variable it sets and the default value (if any). 

{% highlight bash %}
optparse.define short=f long=file desc="The input file" variable=filename
{% endhighlight %}

Flags are defined in exactly the same way, but with an extra parameter `value` that is assigned to the variable. 

{% highlight bash %}
optparse.define short=v long=verbose desc="Set flag for verbose mode" variable=verbose_mode value=true default=false
{% endhighlight %}

###2. Evaluate your arguments
The `optparse.build` function creates a temporary header script based on the provided argument definitions. Simply source the file the function returns, to parse the arguments.

{% highlight bash %}
source $( optparse.build )
{% endhighlight %}

####That's it!
The script can now make use of the variables. Running the script (without any arguments) should give you a neat usage description.
    
	usage: ./script.sh [OPTIONS]
	    
	OPTIONS:
	    
	    -f --file   :  The input file
	    -v --verbose:  Set flag for verbose mode
	    
	    -? --help   :  usage
        
##Supported definition parameters
All definition parameters for `optparse.define` are provided as `key=value` pairs, seperated by an `=` sign.
####`short`
a short, single-letter name for the option
####`long`
a longer expanded option name
####`variable`
the target variable that the argument represents
####`value`(optional)
the value to set the variable to. If unspecified, user is expected to provide a value.
####`desc`(optional)
a short description of the argument (to build the usage description)
####`default`(optional)
the default value to set the variable to if argument not specified

##Installation
1. Download/clone `optparse.bash`
2. Add 

```bash    
`source /path/to/optparse.bash` 
```
to `~/.bashrc`
 
