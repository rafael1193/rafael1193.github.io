---
layout: blogpost
title: SUPREM process simulator for Linux
language: en
---

SUPREM is a 2D semiconductor process simulator made at Stanford University on the early nineties. Actually is the base of most process simulation commercial programs, like SPICE is on circuit simulation.

![SUPREM 4GS running on Fedora 20]({{site.url}}/assets/img/posts/2014-04-15-suprem-process-simulator-for-linux-0.png "SUPREM 4GS running on Fedora 20")

It is not free (as in free speech), because distribution either in source or binary forms cannot be done for money, but you can use it for any other purpose: change the software to suit your needs and share the changes you make.

SUPREM is a really old UNIX software and doesn't compile out&ndash;of&ndash;the&ndash;box on Linux. *Don't blame Linux, he is too young for SUPREM :)*. Makefiles are old, sources depend on raw X11 calls and building needs a GCC 3.x FORTRAN compiler, that is not available on all GNU/Linux distributions.

I am taking an integrated circuit design course this semester, and SUPREM is needed for semiconductor process simulation. Teacher provided us a windows build of SUPREM 4GS, but being SUPREM an UNIX program, it's a sin running it on Wine like a burden Windows program :P

*Cogenda Software* provides updated Makefiles for Linux, but that's not enough and more changes are needed. So I made these changes and SUPREM 4GS version builds with a

{% highlight bash %}
make depend install
{% endhighlight %}

and runs on x86 and x86_64 Linuxes. The only cost it is not having X11 plotting support, that can easily be fixed using [POSTMINI graphical post processor](https://home.comcast.net/~john.faricelli/tcad.htm) available for Linux.

As other sources, [SUPREM for Linux can be downloaded from my github repository](https://github.com/rafael1193/suprem4gs). I would like to make DEB and RPM packages for SUPREM, but I don't know how to do it. Help is needed.
