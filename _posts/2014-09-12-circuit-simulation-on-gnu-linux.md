---
layout: blogpost
title: Circuit simulation on GNU/Linux
language: en
---

Circuit simulation, a daily task for electronic engineers, is not easy on GNU/Linux. Proof of it is I have seen users of free operating systems setting a Windows virtual machine with the only purpose of running PSPICE or LTSPICE. There are several simulators that run on GNU/Linux like Gnucap, ngspice and QUCS. They have very powerful features, but some important flaws are present:

* *QUCS* have a very good QT based GUI, it has a lot of features and it is relatively easy to use. But it is not based on SPICE, the standard on educational and enterprise environments.

* *Gnucap* is another alternative. But its last stable release dates from 2006 and it is command line based only.

* *ngspice* is the successor of the original SPICE3 and it's free/libre but doesn't have a GUI. There are several 3rd party graphical interfaces as gspiceui or easyspice but they doesn't work reasonably well.

So **there are** free circuit simulators but they are not easy to use or don't meet the required criteria of being based on SPICE.

Another important side of circuit simulation is schematic design. In this case, available programs for this are useful and easy to use because they are GUI based. Examples are *gschem* from gEDA and *eeschema* from KiCad suite.

Following schematic design a netlisting software is required for passing circuit information to a simulator. This task can be accomplished by *gnetlist*, again from gEDA suite.

As you can see, there are most of the ingredients necessary for a very good circuit simulation experience: schematic editor, netlister and simulator, but they are not integrated. There is not any free system that could load your schematic, convert it to a netlist, simulate it and show the results with a click. You have to run the process manually.

For instance:

{% highlight bash %}
# Generate a netlist from schematic file
gnetlist -g spice-sdb -o circuit.net -- circuit.sch
# run ngspice on interactive mode and write simulation commands manually
ngspice circuit.cir
# or run ngspice on batch mode and get simulation results from simulation 
# parameters written on netlist
ngspice -b circuit.cir
# numerical results are shown on an ASCII table and plots are given on an ugly
# X11 window or on an even uglier ASCII plot
{% endhighlight %}

There is no option to get this results on a csv file, that could be opened by a spreadsheet program, or save plots on png and svg modern graphic formats.

Additionally, ngspice and gnucap need device models, a set of parameters that define the behavior of a physical component. This is the really, really, really difficult task to solve because there are not free, as in free speech, device model definitions. They are published by manufacturers with unclear and potentially non-free licenses. Some SPICE parameters can be extracted from devices, but not all of them. Non-free content cannot be included on free operating systems like Ubuntu, Debian or Fedora, so this is a big issue that cannot be solved without device manufacturer implication.

![SpiceGUI showing simulation results](https://cloud.githubusercontent.com/assets/436547/4139264/0a6d404a-3399-11e4-9ac1-92799f66ba3b.png "SpiceGUI showing simulation results")

The solution I propose is *SpiceGUI*. A program that aims to make circuit simulation on GNU/Linux operating systems easier with a modern and easy to use graphical user interface. *SpiceGUI* makes more straightforward the process from schematic editing to result analysis with a Gtk 3 interface that doesn't look as an alien as all other (Windows and Linux) simulation GUIs do. (Yes, there are a lot of Windows-based GUI circuit simulation tools, but all of them graphically sucks)

**You can try *SpiceGUI* building it from [source](https://github.com/rafael1193/spicegui/releases) or installing its [RPM package](https://github.com/rafael1193/spicegui/releases)**
