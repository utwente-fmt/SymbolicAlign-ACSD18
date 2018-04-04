# SymbolicAlign-ACSD18
Symbolically Aligning Observed and Modelled Behaviour
===

This repository hosts the experiments and results for the paper and provides a
short guide on how to install the tools and reproduce the results.

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
alignments applies the A* shortest path algorithm for each trace of event data.

*In this work, we apply insights from the field of model checking to aid
conformance checking. We investigate whether alignments can be computed
efficiently via symbolic reachability with decision diagrams. We designed a
symbolic algorithm for computing shortest-paths on graphs restricted to 0- and
1-cost edges (which is typical for alignments).

*We have implemented our approach in the LTSmin model checking toolset and
compare its performance with the A* implementation supported by ProM.  We
generated more than 4000 experiments (Petri net model and log trace
combinations) by setting various parameters, and analysed performance and
related these to structural properties.

*Our empirical study shows that the symbolic technique is in general better
suited for computing alignments on large models than the A* approach. Our
approach is better performing in cases where the size of the state-space tends
to blow up.  Based on our experiments we conclude that the techniques are
complementary, since there is a significant number of  cases where A*
outperforms the symbolic technique and vice versa.

Installation
---

The source code for the Symbolic alignment algorithm is obtained by the
following command:
* `$ git clone git@github.com:vbloemen/ltsmin.git -b acsd18 --recursive`

If you experience any issues with the installation please consult the [LTSmin] 
website for further instructions. Otherwise, please contact the first author
([Vincent Bloemen](mailto:v.bloemen@utwente.nl)) for further help.

Data
---

All data used in the paper is available at the 4TU data centre, with the DOI:
10.4121/uuid:a6709ee4-2aa3-49a3-92db-247e8b5bf340 (under verification).


[LTSmin]: http://fmt.cs.utwente.nl/tools/ltsmin/
[ACSD 2018]: https://interes.institute/acsd2018/








