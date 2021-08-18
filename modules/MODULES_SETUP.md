# MODULES SYSTEM 


It can be convienent to have modules setup on your development workstation especially if you use multiple different compilers or libraries. 

Modules is the same system that many clusters use. The open source website can be found [here](http://modules.sourceforge.net/). 



## Installation
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

## Items with prepared module files 

In my experiance CASLAB users particularly those using the GEMS solver require use of either the Intel compilers or its associated Math Kernal Library(MKL). Traditionally after installation the environment of the OneAPI tool kit is set by calling

```bash
    source /opt/intel/oneapi/setvars.sh
```

Looking at this file the details are staggering. Fortunatly Intel has done most of the heavy lifting for us. Now with no modules loaded if we try to call the Intel C compiler:

```bash
    >which icc
    Command 'icc' not found
```
To setup the module files first 
```bash
    >cd /opt/intel/oneapi
    >modulefiles-setup.sh
```
we can then add the new module file directory as 
```bash
    >module use /opt/intel/oneapi/modulefiles
```

Now when we call <code>module avail</code> we get 

```bash
    module avail
----------------------------------------------------- /opt/intel/oneapi/modulefiles ------------------------------------------------------
advisor/2021.1.1        compiler/latest         dnnl-cpu-iomp/2021.1.1  init_opencl/latest            itac/2021.1.1     tbb/latest      
advisor/latest          compiler32/2021.1.1     dnnl-cpu-iomp/latest    inspector/2021.1.1            itac/latest       tbb32/2021.1.1  
ccl/2021.1.1            compiler32/latest       dnnl-cpu-tbb/2021.1.1   inspector/latest              mkl/2021.1.1      tbb32/latest    
ccl/latest              dal/2021.1.1            dnnl-cpu-tbb/latest     intel_ipp_ia32/2021.1.1       mkl/latest        vpl/2021.1.1    
clck/2021.1.1           dal/latest              dnnl/2021.1.1           intel_ipp_ia32/latest         mkl32/2021.1.1    vpl/latest      
clck/latest             debugger/10.0.0         dnnl/latest             intel_ipp_intel64/2021.1.1    mkl32/latest      vtune/2021.1.1  
compiler-rt/2021.1.1    debugger/latest         dpct/2021.1.1           intel_ipp_intel64/latest      mpi/2021.1.1      vtune/latest    
compiler-rt/latest      dev-utilities/2021.1.1  dpct/latest             intel_ippcp_ia32/2021.1.1     mpi/latest        
compiler-rt32/2021.1.1  dev-utilities/latest    dpl/2021.1.1            intel_ippcp_ia32/latest       oclfpga/2021.1.1  
compiler-rt32/latest    dnnl-cpu-gomp/2021.1.1  dpl/latest              intel_ippcp_intel64/2021.1.1  oclfpga/latest    
compiler/2021.1.1       dnnl-cpu-gomp/latest    init_opencl/2021.1.1    intel_ippcp_intel64/latest    tbb/2021.1.1      

----------------------------------------------------- /usr/share/modules/modulefiles -----------------------------------------------------
dot  module-git  module-info  modules  null  use.own  
```
We now can load an unload any of the component parts of oneAPI and see their path correctly 

```bash
    >module load compiler/latest
    >which which icc
    /opt/intel/oneapi/compiler/2021.1.1/linux/bin/intel64/icc
```

or see the enviroment variable for the MKL

```bash
    >module load mkl
    >echo $MKLROOT 
    /opt/intel/oneapi/mkl/2021.1.1
```