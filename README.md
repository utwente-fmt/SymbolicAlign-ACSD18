# Symbolically Aligning Observed and Modelled Behaviour


This repository hosts the results for the paper.

Please note that all experiments in the paper were performed on an
Intel Core<sup>TM</sup> i7-4710MQ processor with 2.50GHz and 7.4Gib memory,
running Debian Stretch.

Submitted and accepted by [ACSD 2018].

Authors:
---

* Formal Methods and Tools, University of Twente, The Netherlands
    - Vincent Bloemen*:      [<v.bloemen@utwente.nl>](mailto:v.bloemen@utwente.nl)
    - Jaco van de Pol:       [<j.c.vandepol@utwente.nl>](mailto:j.c.vandepol@utwente.nl)

* Process and Data Science, RWTH Aachen University, Germany
    - Wil van der Aalst: [<wvdaalst@pads.rwth-aachen.de>](mailto:wvdaalst@pads.rwth-aachen.de)

\* Supported by the 3TU.BSR project.

Abstract
---
*Conformance checking is a branch of process mining that aims to assess to what
degree a given set of log traces and a corresponding reference model conform to
each other. The state-of-the-art approach in conformance checking is based on
the concept of alignments. Alignments  express the observed behaviour in terms
of the reference model while minimizing the number of mismatches between the
event data and the model. The currently known best algorithm for constructing
alignments applies the A&ast; shortest path algorithm for each trace of event
data.*

*In this work, we apply insights from the field of model checking to aid
conformance checking. We investigate whether alignments can be computed
efficiently via symbolic reachability with decision diagrams. We designed a
symbolic algorithm for computing shortest-paths on graphs restricted to 0- and
1-cost edges (which is typical for alignments).*

*We have implemented our approach in the LTSmin model checking toolset and
compare its performance with the A&ast; implementation supported by ProM.  We
generated more than 4000 experiments (Petri net model and log trace
combinations) by setting various parameters, and analysed performance and
related these to structural properties.*

*Our empirical study shows that the symbolic technique is in general better
suited for computing alignments on large models than the A&ast; approach. Our
approach is better performing in cases where the size of the state-space tends
to blow up.  Based on our experiments we conclude that the techniques are
complementary, since there is a significant number of  cases where A&ast;
outperforms the symbolic technique and vice versa.*

## Installation
---
We provide installation details below for a Linux system (we tested this on
Debian Stretch 9).

### Installing dependencies
* `sudo apt-get install build-essential automake autoconf libtool libpopt-dev
zlib1g-dev zlib1g flex ant asciidoc xmlto doxygen wget git bison cmake
libgmp-dev libhwloc-dev`

### Obtain the this git repository
* `git clone https://github.com/utwente-fmt/SymbolicAlign-ACSD18.git`
* `cd SymbolicAlign-ACSD18`

### Install Sylvan (more information: https://trolando.github.io/sylvan/)
* `git clone https://github.com/utwente-fmt/sylvan.git -b v1.1.0`
* `cd sylvan`
* `mkdir build`
* `cd build`
* `cmake ..`
* `make && make test && sudo make install`
* `cd ../..`


### Install LTSmin (more information: http://ltsmin.utwente.nl/)
* `git clone https://github.com/vbloemen/ltsmin.git -b acsd18 --recursive`
* `cd ltsmin`
* `./ltsminreconf`
* `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib    # to find libsylvan.so`
* `./configure --without-doxygen --disable-dependency-tracking PCK_CONFIG_PATH="/opt/local/lib/pkgconfig"`
* `make`
* `sudo make install`

### Installing the helper tool (written in Go)
The binary file `pnmlprod` in the current repository should work for most linux
distributions, otherwise, the program can be obtained at:
* `go get github.com/vbloemen/pnmlprod`

(Please make sure that you have a working Go installation and make sure that
$GOPATH/bin is in your PATH)

If you experience any issues with the installation please consult the linked
websites for further instructions. Otherwise, please contact the first author
([Vincent Bloemen](mailto:v.bloemen@utwente.nl)) for further help.


Running Experiments
---

The `test` directory contains an example model (`test/model.pnml`) and XES log
file (`test/log.xes`). You can create a synchronous product of the model and
each log trace in the log file by using the command (the last argument is the
directory for the output files):

* `pnmlprod -p test/model.pnml test/log.xes test`

This will generate synchronous products for the model and every log trace in
`test/log.xes`. It also generates DOT files, that represent the model and
synchronous products.

The symbolic algorithm can then be used with the following command:

* `pnml2lts-sym --edge-label=name --order=align --trace=trace.txt
  --align-variant=double-smallest test/syncmodel-0.pnml`

Which will generate a `trace.txt.gcf` file, which can be converted to a
human-readable `trace.txt` file with:

* `ltsmin-printtrace -q trace.txt.gcf > trace.txt`

Which can finally be converted into an alignment using the `pnmlprod` tool:

* `pnmlprod -a test/syncmodel-0.pnml trace.txt`

Which will look similar to the following:

```(» | τ : n92)
(l | l : logs0n0)
(» | τ : n109)
(h | h : logs1n0)
(t | t : logs2n1)
(d | d : logs3n0)
(» | τ : n110)
(d | » : logt4)
(i | i : logs5n0)
(r | r : logs6n0)
(» | τ : n93)
(» | τ : n133)
```

Data
---

All data used in the paper is available at the 4TU data centre:
https://doi.org/10.4121/uuid:a6709ee4-2aa3-49a3-92db-247e8b5bf340


[LTSmin]: http://fmt.cs.utwente.nl/tools/ltsmin/
[ACSD 2018]: https://interes.institute/acsd2018/








