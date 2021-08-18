# MODULES SYSTEM 


It can be convienent to have modules setup on your development workstation especially if you use multiple different compilers or libraries. 

Modules is the same system that many clusters use. The open source website can be found [here](http://modules.sourceforge.net/). 



## Instalation
More detailed installation instructions can be found on the website. However for most CASLAB users Ubuntu is the default operating system. For this we can just use <code> apt-get </code>

```bash
    sudo apt-get install environment-modules
```

Counterintuitively this installation does not add <code>module</code> commands to the path by default. To include it we must source the bash or csh script (depending on your shell type)

```bash
    source /etc/profile.d/modules.sh
```

The required changes to your config files (e.g.<code>.bashrc</code>) by 

```bash
    add.modules
```

You should now be able to use the <code> module </code> commands

## Setting a Default Module path

The default module are stored at <code>/usr/share/modules/modulefiles </code>
 
You should add the folowing to your <code>.bashrc</code> (or equivelent)
```bash
    export MODULEPATH='/usr/share/modules/modulefiles'
```
I also personally recommend removing all extra aspects of your <code>$PATH</code>
such as
```bash
    unset PATH
    export PATH='/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin'
```

## Setting up a module






## Items with prepared module files 

In my experiance CASLAB users particularly those using the GEMS solver require use of either the intel compilers or its associate Math Kernal Library(MKL). Traditionally after installation of the OneAPI tool kit by calling

```bash
    source /opt/intel/oneapi/setvars.sh
```

Looking at this file the details are staggering. Fortunatly 


