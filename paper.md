---
title: 'Logic Programming Working Group'
tags:
  - logic programming
authors:
  - name: Chris Mungall
    orcid: 0000-0002-8021-9162
    affiliation: 1
  - name: Hirokazu Chiba
    affiliation: 2
  - name: Pjotr Prins
    orcid: 0000-0002-8021-9162
    affiliation: 3
  - name: Nada Amin
    affiliation: 4
  - name: Deepak Unni
    affiliation: 5
  - name: William E. Byrd
    affiliation: 6
affiliations:
  - name: Molecular Ecosystems Biology, Berkeley Lab, USA
    index: 1
  - name: Database Center for Life Science, Research Organization of Information and Systems, Japan
    index: 2
  - name: Department of Genetics, Genomics and Informatics, The University of Tennessee Health Science Center, Memphis, TN, USA.
    index: 3
  - name: Please fill in
    index: 4
  - name: Please fill in
    index: 5
  - name: University of Alabama, USA
    index: 6
date: 28 December 2019
bibliography: paper.bib
---

<!--

The paper.md, bibtex and figure file can be found in this repo:

  https://github.com/journal-of-research-objects/Example-BioHackrXiv-Paper

To modify, please clone the repo. You can generate PDF of the paper by
pasting above link (or yours) in

  http://biohackrxiv.genenetwork.org/

-->

# Introduction

Logic programming in the form of relational SQL queries on database
tables and and SPARQL queries on semantic web graph data stores, is
well known to many bioinformaticians. More advanced logic programming,
however, is underutilized in bioinformatics.  Prolog, for example, is
a high-level programming language that has its roots in first-order
logic or first-order predicate calculus and Minikanren is an embedded
Domain Specific Language for logic programming. Interestingly, the
core miniKanren language is very simple, with only three logical
operators and one interface operator[@ReasonedSchemer].

![Logic programming resolver traverses the solution space to find all matches \label{fig}](./logic-programming.png)

The introducting of logic programming is particularly relevant in the
context of multi-model data representations where data can be accessed
in memory as free data structures, but also on disk where data can be
represented as tables, trees (documents), and graphs. In
bioinformatics we can make use of all these different data sources and
have a query engine that can mine them all efficiently.

Logic programming fits biological research really well. Essentially, a
researcher writes a number of statements with variables and the logic
engine will go through the solution space (all data) and find the
matches (see figure \ref{fig}). Much more detail on the rationale and
implementations of miniKanren and logic programming are well
summarized in Byrd's book The Reasoned Schemer [@ReasonedSchemer], his
PhD thesis [@ByrdPhD] (or one of Byrd's online talks).

The 'Logic Programming' working group at the 2019 edition of Japanese
Biohackathon researched state-of-the-art mapping between graph stores;
created methods for bridging between SPARQL and in-memory data
representations using Prolog; extended the Biolink model and added
Relational Biolink type inference for mediKanren.

<!--
# Results
-->

## Existing logic programming facilities for SPARQL

We researched current solutions for combining logic programming with
SPARQL.
[ClioPatria](http://www.semantic-web-journal.net/system/files/swj1074.pdf)
is an in-memory RDF quad-store tightly coupled with SWI-Prolog by Jan
Wielemaker the main author of SWI-Prolog[@WielemakerBHO15]. SWI-Prolog
is published under a BSD license and there exist even bindings for
[ClioPatria and Python](http://wi.hwtk.de/WLP2018/Papers/WLP_2018_paper_4.pdf),
for example, though the repo is not found yet. We think ClioPatria and
SWI-Prolog are particularly useful for teaching and (in-memory)
semantic web applications. SWI-Prolog comes with client libraries for
SQL and SPARQL queries.

## Application of SPARQLProg to biological databases

<!--
    State the problem you worked on
    Give the state-of-the art/plan
    Describe what you have done/results starting with The working group created...
    Write a conclusion
    Write up any future work
-->


A number of biological databases have been developed on the basis of
RDF supporting SPARQL access, including
[Uniprot](https://www.uniprot.org/),
[NCBI Pubchem](https://pubchemdocs.ncbi.nlm.nih.gov/rdf) and the
[EBI RDF platform](https://www.ebi.ac.uk/rdf/). Complicated SPARQL
queries are required to effectively extract information combining such
databases. Composing complex SPARQL queries is bothersome work due to
the lack of abstract modularized structure in SPARQL. Thus, high-level
programming methodology on the basis of SPARQL endpoints is wished
for.  Here, we use
[SPARQLProg](https://github.com/cmungall/sparqlprog) by Chris Mungall
to compose building blocks to realize high-level programming by
wrapping access to existing SPARQL endpoints in the form of Prolog
code. The examples we developed include programs accessing RDF databases of MBGD [@Uchiyama:2019], KEGG OC,
TogoVar, JCM, Allie, EBI BioSamples, UniProt, and DisGeNET. Future
work includes using these Prolog codes as building blocks for
integrative analysis. SPARQLProg is written in
SWI-Prolog and has a Python interface library. All code has been made
available in the example directory of
[SparqlProg](https://github.com/cmungall/sparqlprog) which provides
sophisticated mapping of logic queries to SPARQL.

## Extending the BioLink Model

<!--
    State the problem you worked on
    Give the state-of-the art/plan
    Describe what you have done/results starting with The working group created...
    Write a conclusion
    Write up any future work
-->

The [BioLink Model](https://github.com/biolink/biolink-model) is a
data model developed for representing biological and biomedical
knowledge. It represents a schema and generated objects for biolink
data model and upper ontology. It was designed with the goal of
standardizing the way information is represented in a graph store
regardless of the formalism used. The working group focused on
extending this model to support representation of a wide variety of
knowledge.

The following tasks were accomplished as part of the Biohackathon:

1) represent Datasets, and its related metadata
2) represent Family and Pedigree information, to support clinical knowledge
3) make the provenance model more rich and descriptive

For future work, the group will ensure that the new classes added to
the model will have appropriate mappings to other schemas and
ontologies.

##  Relational Biolink type inference for mediKanren

<!--
    State the problem you worked on
    Give the state-of-the art/plan
    Describe what you have done/results starting with The working group created...
    Write a conclusion
    Write up any future work

* Remote member Nada Amin, Chris Mungall, Deepak Unni, Will Byrd

-->


* Goal: implement a relational type inferencer for the Biolink model in miniKanren, which can be integrated into mediKanren

* Nada added a `yaml` subdirectory to the mediKanren GitHub page, and created multiple files:

https://github.com/webyrd/mediKanren

** `yaml2sexp.py` generates the `biolink.scm` file, which contains an s-expression version of the Biolink yaml file

** `yaml.scm` contains miniKanren relations, and Chez Scheme code that generates miniKanren relations based on `biolink.scm` (basically these are giant `conde` clauses that can be though of as relational tables);  `yaml.scm` also contains tests for the relations.

Chris and Deepak are guiding us wrt the Biolink semantics

Future work

* integrate into the Racket mediKanren code

* integrate with the data categories in the KGs

* create query editor with decent type error messages, autocomplete, query synthesis, etc.

# Discussion

The working group concluded that there is ample scope for logic
programming in bioinformatics. Future work inludes expansion of
accessing semantic web databases using adding SPARQLProg, expanding
the Biolink model and adding dynamic SPARQL support to miniKanren.

# References
