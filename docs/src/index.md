# CUTEst.jl documentation

This package provides an interface to
[CUTEst](http://ccpforge.cse.rl.ac.uk/gf/project/cutest/wiki),
the *Constrained and Unconstrained Test Environment with safe threads*
for nonlinear optimization.

This package uses
[NLPModels.jl](https://github.com/JuliaSmoothOptimizers/NLPModels.jl), but it
also gives direct access to the CUTEst functions.

## CUTEst brief history

CUTEst has been around for a while. It started as CUTE, then CUTEr,
then CUTEr2, and finally CUTEst.
The [original project](https://ccpforge.cse.rl.ac.uk/gf/project/cutest/) can be
used independently of Julia.

CUTEst works by decoding a `.SIF` file into other files and objects so that a
user compiles links that to his code. It also gives the option of doing that
for you, in which case you have to send some code to it's folder, and ask for
the compilation.

CUTEst gives you about 100 methods to access the objective and constraints
functions, as well as their derivatives in many different formats. It also gives
access to the problem's information, like number of variables, constraints, the
initial point, the bounds, an so on.

## Installing

On Linux, you'll need to install `wget` and `gfortran`, and possibly have to fix the location of `libgfortran.so`.

On Ubuntu 14.04, you can do this with
```
sudo apt-get install wget gfortran
sudo ln -s /usr/lib/gcc/x86_64-linux-gnu/$(gfortran -dumpversion | cut -f1,2 -d.)/libgfortran.so /usr/local/lib
```
On Ubuntu 16.04,
```
sudo apt-get install wget gfortran
sudo ln -s /usr/lib/x86_64-linux-gnu/libgfortran.so.3 /usr/local/lib/libgfortran.so
```
On Archlinux, do
```
sudo pacman -S wget gfortran
```

The following commands should automatically download and install CUTEst and its
dependencies.
````julia
Pkg.add("CUTEst")
````

## Usage

Check the [tutorial](tutorial) for complete usage.

The simplest use of CUTEst is through the interface of NLPModels.jl.
Here's the quick [reference
guide](https://github.com/JuliaSmoothOptimizers/NLPModels.jl/api#reference-guide).

```@example
using CUTEst

nlp = CUTEstModel("ROSENBR")
println("x0 = $(nlp.meta.x0)")
println("fx = $( obj(nlp, nlp.meta.x0) )")
println("gx = $( grad(nlp, nlp.meta.x0) )")
println("Hx = $( hess(nlp, nlp.meta.x0) )")
finalize(nlp)
```

Check the [NLPModels API](api/#nlpmodels-api) for details.

## Working with CUTEst directly

We also have implemented function to allow access to the CUTEst functions
directly. There is a specialized API which provides a Julian way to access them,
and a core API which is only a wrapper for CUTEst.
For more information see the section [core](core), or
the documentation [here](api/#core-and-specialized-api).

## Contents

```@contents
```
