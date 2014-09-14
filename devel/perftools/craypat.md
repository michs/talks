name: title-slide
class: center, middle, inverse
layout: true
---
name: section-slide
class: left, middle, inverse
layout: true
---
name: default
class: left, top
layout: true
---
name: title
template: title-slide

Performance Analysis with CrayPat
=================================
<p>&nbsp;</p>
Working Notes
-------------
<p>&nbsp;</p>
Michael Schliephake, 2014-09-14

.footnote[
Navigate with arrow keys&nbsp;&nbsp;<-&nbsp;&nbsp;->]
---
## General Information

Manual _Using Cray Performance Measurement and Analysis Tools_
* Online documentatin for Milner: [CrayPat V. 6.2.1](http://docs.cray.com/books/S-2376-621/)

### Preparing the analysis
* Load/swap `PrgEnv` module
* Environment must be set after logging in
* Re-compile resp. re-link your program for instrumentation (when switching between tools)

#### Environment for PrgEnv-cray

```bash
# PrgEnv-cray/5.1.29 is loaded initially
module swap cce/8.2.3 cce/8.3.3
module swap cray-mpich/6.2.1 cray-mpich/7.0.3
module load perftools/6.2.1   # or perftools-lite/6.2.1
```
---
### Preparing the analysis (ctd.)

#### Environment for PrgEnv-intel

```bash
# PrgEnv-cray/5.1.29 is loaded initially
module swap PrgEnv-cray/5.1.29 PrgEnv-intel/5.1.29
module swap cray-mpich/6.2.1 cray-mpich/7.0.3
module load perftools/6.2.1   # or perftools-lite/6.2.1
```

#### Environment for PrgEnv-gnu

```bash
# PrgEnv-cray/5.1.29 is loaded initially
module swap PrgEnv-cray/5.1.29 PrgEnv-gnu/5.1.29
module swap cray-mpich/6.2.1 cray-mpich/7.0.3
module load perftools/6.2.1   # or perftools-lite/6.2.1
```
---
## About the examples in this presentation

* An MPI implementation of parallel sorting algorithm has been used in the examples, executed with 20 ranks on 2 nodes

* Name scheme of generated files during the performance analysis
  
    <tt>a.out+PID-node[s/t].xf</tt>

    Examples use concrete names from runs instead of symbolic ones

|         |   |                                                               |
|:--------|---|:--------------------------------------------------------------|
|__a.out__|   | name of the instrumented executable                           |
|__PID__  |   | process ID of to the instrumented executable                  |
|__node__ |   | node ID of rank zero.                                         |
|__s/t__  |   | type of te experiment, either s for sampling or t for tracing |
---
template: section-slide
.right-column[
# CrayPat-lite
]
---
## CrayPat-lite: Usage
Manual section 1.2: _About CrayPat-lite_
_ _ _
#### Example session first analysis
```bash
make a.out
aprun -n 20 -N 10 ./a.out
# Find most recent created report and look at it
ls -ltr \*.rpt 
less a.out+135727-8s.rpt 
```
#### Example session applying event tracing
```bash
export CRAYPAT_LITE=event_profile
make a.out
aprun -n 20 -N 10 ./a.out
# Find most recent created report and look at it
ls -ltr
less a.out+135729-8t.rpt
# Note also if information about improved rank placement has been generated
less MPICH_RANK_ORDER.USER_Time
less MPICH_RANK_ORDER.USER_Time_hybrid 
```
---
template: section-slide
.right-column[
# CrayPat
]
---
## CrayPat: Usage for automatic profiling I
Manual section 2.1: _Basic Profiling_
_ _ _
#### Example session
```bash
# The preparation as usual
module unload perftools-lite/6.2.1  # if previously loaded
module load perftools/6.2.1
make a.out
# Instrument the program and execute a first run
pat_build a.out
aprun -n 20 -N 10 ./a.out+pat
# Find the collected data and process with pat_report
ls -ltr *.xf
pat_report a.out+pat+135731-8s.xf | tee info-135731.txt
```
* Sampling based report in <tt>info-135731.txt</tt>
* <tt>pat_build</tt> arguments for further analysis in <tt>apa</tt> file (here <tt>a.out+pat+135731-8s.apa</tt>)
* Cray Apprentice2 in <tt>s.ap2</tt> file (here <tt>a.out+pat+135731-8s.ap2</tt>)
---
## CrayPat: Usage for automatic profiling II
#### Example session (ctd.)

```bash
# Re-build for tracing analysis and re-run the program
pat_build -O a.out+pat+135731-8s.apa
aprun -n 20 -N 10 ./a.out+apa
# Find the collected data and process with pat_report
ls -ltr
pat_report a.out+apa+135732-8t.xf | tee info-135732.txt
```
* Tracing based report in <tt>info-135732.txt</tt>
* Cray Apprentice2 in <tt>t.ap2</tt> file (here <tt>a.out+apa+135732-8t.ap2</tt>)

We can run with an optimised MPI rank order once more and look at the differences to the provious run now.

```bash
ls -ltr MPICH_RANK_ORDER*
cp MPICH_RANK_ORDER.USER_Time MPICH_RANK_ORDER
export MPICH_RANK_REORDER_METHOD=3
aprun -n 20 -N 10 ./a.out+apa
unset MPICH_RANK_REORDER_METHOD
ls -ltr *.xf
pat_report a.out+apa+135793-100t.xf | tee info-135793.txt
```
---
## CrayPat: Tracing parts of a program I
### Predefined groups
* Manual section 2.2: _Using Predefined Groups_
* See the manual for a list of predefined groups

#### Example session

```bash
pat_build -g mpi a.out
aprun -n 20 -N 10 ./a.out+pat
pat_report a.out+pat+135797-100t.xf | tee info-135797.txt
```
---
## CrayPat: Tracing parts of a program II
### User-defined Functions
* Manual section 2.3: _Tracing User-defined Functions_
* Several options allow to choose functions to include or exclude in the tracing, name lists can be specified in a file

#### Example session for tracing of all user functions
* Compile the code using the option ``-finstrument-functions`` for GNU and Intel, use ``-h profile_generate`` for Cray compilers
* Option ``-w`` turns on the tracing API

```bash
make a.out              # with activated instrumentation for compilation
pat_build -w -g mpi a.out  # trace user and MPI functions
```
Alternatively
```bash
pat_build -u -g mpi a.out  # mentioned compiler options not necessary
```
---
## CrayPat: Hardware performance counters

Check availability of counters
```bash
aprun -n 1 papi_avail
aprun -n 1 papi_native_avail
```
Define a selection of counters before running the ``a.out+pat``
```bash
export PAT_RT_PERFCTR=PAPI_LD_INS,PAPI_SR_INS
```
Also groups of predefined counters are available, see ``man hwpc``
```bash
export PAT_RT_PERFCTR=1
```
---
## CrayPat: Some specific analyses

### Profile line by line

```bash
pat_build a.out  # without any options
aprun -n 20 -N 10 ./a.out+pat
pat_report -O samp_profile+src
```

### Collecting as much as possible data
Disables data aggregation during runtime (creates large amounts of tracing data), enables mosaic and traffic view in Cray Apprentice2

```bash
pat_build -g mpi a.out
export PAT_RT_SUMMARY=0
aprun -n 20 -N 10 ./a.out+pat
```
---
## The CrayPat API

\[TODO\]
---
## Analysing OpenMP programs with CrayPat

\[TODO\]
---
## Cray Reveal: Analysis of hybrid OpenMP/MPI programs

\[TODO\]
