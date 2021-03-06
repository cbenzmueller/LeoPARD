LeoPARD
=======
*Leo-III's Parallel ARchitecture and Datastructures*

This project contains the data structure framework LeoPARD underlying the Leo-III prover.

In the Leo-III project, we design and implement a state-of-the-art
Higher-Order Logic Theorem Prover, the successor of the well known
LEO-II prover
[[1](http://dx.doi.org/10.1007/978-3-540-71070-7_14)]. Leo-III will be
based on ordered paramodulation/superposition. The prover also
integrates and extends ideas from LEO-I
[[2](http://dx.doi.org/10.1007/BFb0054256)] and the OANTS
[[3](http://dx.doi.org/10.1016/j.jal.2007.06.003),[4](http://dx.doi.org/10.1007/BFb0057438)]
blackboard mechanism.  In contrast to LEO-II and LEO-I, we replace the
internal term representation (the commonly used simply typed
lambda-calculus) by a more expressive system supporting type
polymorphism.  In order to achieve a substantial performance speed-up,
the architecture of Leo-III will be based on massive parallelism
(e.g. And/Or-Parallelism, Multisearch)
[[5](http://dx.doi.org/10.1023/A:1018932114059)]. The current design
is a multi-agent blackboard architecture that will allow to
independently run agents with our proof calculus as well as agents for
external (specialized) provers.  Leo-III will focus right from the
start on compatibility to the widely used TPTP infrastructure
[[6](http://dx.doi.org/10.1007/s10817-009-9143-8)]. Moreover, it will
offer built-in support for specialized external prover agents and
provide external interfaces to interactive provers such as
Isabelle/HOL [[7](http://dx.doi.org/10.1007/3-540-45949-9)]. The
implementation will excessively use term sharing
[[8](http://dl.acm.org/citation.cfm?id=1218621),
[9](http://dl.acm.org/citation.cfm?id=1218620)] and several indexing
techniques [[10](dx.doi.org/10.1007/3-540-45744-5_19),
[11](dx.doi.org/10.1007/978-3-540-71070-7_14)]. Leo-III will also
offer special support for reasoning in various quantified
non-classical logics by exploiting a semantic embedding
[[12](dx.doi.org/10.5220/0004324803460351)] approach.

As a test and for illustration purposes, a small executable can be created than runs a basic
propositional reasoning process. After the public release of Leo-III further features of this
prover will be made available in LeoPARD.

Further information can be found at the [Leo-III
Website](http://page.mi.fu-berlin.de/lex/leo3/).

Features
----------------

- Basic standard data structures for logical reasoning included (such as Terms, Clauses, Literals, Signatures, ...)
- Efficient higher-order term representation based on the polymorphically typed Lambda-Calculus (employing Spine notation, explicit substitutions and perfect term sharing) 
- Parser for every TPTP syntax dialect (including CNF, FOF, TFF, TFA, TH0), preliminary support for TFF1-draft dialect
- Translation module for transforming each parsed formula to an equivalent Lambda-Term
- Backward translation of internal terms and formulae to TPTP THF compatible representation
- Signature with all TPTP-compatible (fixed/defined) constants available
- Generic multi-agent design for massive parallel reasoning
- Generic templates for the employment of external reasoners included (works best with SZS status compatible reasoners)
- Blackboard architecture for agent communication and knowledge sharing

External prover support
----------------

An experimental external prover support is included in this version.
The command-line parameter "--with-prover" can be set to "leo2", "satallax" or "remote-leo2".
In the first two cases the provers need to be installed locally and their paths (the path to the executable) need to be accessible via the environment variables $LEO2_PATH and $SATALLAX_PATH (respectively).
For the remote-leo2 call, internet connection needs to be active.

Related Documents
----------------

- [Max Wisniewski, **Agent-based Blackboard Architecture for a Higher-Order Theorem Prover**. *Master Thesis, Freie Universität Berlin*](http://userpage.fu-berlin.de/~lex/drop/wisniewski_architecture.pdf)
- [Alexander Steen, **Efficient Data Structures for Automated Theorem Proving in Expressive Higher-Order Logics**. *Master Thesis, Freie Universität Berlin*](http://userpage.fu-berlin.de/~lex/drop/steen_datastructures.pdf)
- [Max Wisniewski, Alexander Steen, Christoph Benzmüller, **The Leo-III Project**. *Joint Automated Reasoning Workshop and Deduktionstreffen, 2014*](http://page.mi.fu-berlin.de/cbenzmueller/papers/W53.pdf)
- Yves Müller, **Subprover Parallelism in the Automated Theorem Prover LEO-II**. *Master Thesis, Freie Universität Berlin*, 2013
 

Required Dependencies
----------------

Leo III needs Java 1.7 to run.
Scala 2.11.X is required to build and run the project. Maven will automatically download scala and further dependencies.
Alternatively, Scala can be downloaded at [Scala-lang.org](http://scala-lang.org/download/).


Building the project
----------------

[Maven](http://maven.apache.org/) manages the build process of Leo-III. Information about downloading and installing Maven can be found at [the download section of the maven website](http://maven.apache.org/download.cgi).

The project is compiled and built into an executable `.jar` file usng

    > mvn compile assembly::single

Or, alternatively, the makefile can be used. Invoking

    > make

will result in the same `.jar`
    
All test suits are ran by
    
    > mvn test
    
The compiled test class files will be placed at `./target/test-classes/`.

**For the tests it is important that the project is placed in a path where each directory does not contain any blank spaces. Otherwise the tests are not executed.**

The sole compilation process can be started by typing

    > mvn compile

The compiled files (class files) will be placed at `./target/classes/`.


Project's current structure
--------------

This section is a stub. It will be expanded in the future.

```
└──leo                     -- Where the Main executable is located, root package
    ├── agents             -- Specification of agents
    │   └── impl           -- Implementation of agents
    ├── datastructures     -- root package for all base data structures
    │   ├── blackboard
    │   ├── context
    │   ├── impl           -- Most of the implementations are located here
    │   ├── term
    │   └── tptp           -- Internal syntax representation of TPTP
    └── modules            -- All sorts of functionality modules
        ├── churchNumerals -- old package, most likely to be removed soon
        ├── normalization
        ├── output         -- Output and logging functionality
        ├── parsers        -- Input parsing
        ├── proofCalculi
        └── visualization
```
