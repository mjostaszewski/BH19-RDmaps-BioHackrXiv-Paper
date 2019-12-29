---
title: 'Logic Programming Working Group'
tags:
  - logic programming
authors:
  - name: Chris Mungall
    orcid: 0000-0002-8021-9162
    affiliation: 1
  - name: Pjotr Prins
    orcid: 0000-0002-8021-9162
    affiliation: 2
  - name: Hirokazu Chiba
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
  - name: Department of Genetics, Genomics and Informatics, The University of Tennessee Health Science Center, Memphis, TN, USA.
    index: 2
  - name: National Institute for Basic Biology | NIBB · Laboratory of Genome Informatics, Japan
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

# Introduction

'''Introduction on logic programming and projects for the Biohackathon'''

Logic programming allows for powerful queries. During Biohackathon
2019 we made a show case based on existing facilities for using
logic programming in conjunction with SPARQL.

-![Logic programming resolver](logic-programming.png)


'''Short discussion on state of the art'''

[ClioPatria](http://www.semantic-web-journal.net/system/files/swj1074.pdf)
by Jan Wielemaker the main author of SWI-Prolog. Amazingly, there
exist even bindings for
[ClioPatria and Python](http://wi.hwtk.de/WLP2018/Papers/WLP_2018_paper_4.pdf),
for example, though the repo is not found yet.

# Results

## Application of SPARQLProg to biological databases

[SparqlProg](https://github.com/cmungall/sparqlprog) which provides
sophisticated mapping of logic queries to SPARQL.

Recently, a number of biological databases have been developed on the
basis of RDF supporting SPARQL access. For effectively extracting
information by combining these databases, writing complicated SPARQL
queries are required. However, composing complex SPARQL queries is
bothersome work due to the lack of abstract modularized structure in
SPARQL. Thus, high-level programming methodology on the basis of
SPARQL endpoint is necessary.  Here, we use SPARQLProg technology to
compose building blocks to realize high-level programming by wrapping
access to existing SPARQL endpoints as Prolog code. The examples we
developed include MBGD, KEGG OC, TogoVar, JCM, Allie, EBI BioSamples,
UniProt, and DesGeNET. Future work includes using these Prolog codes
as building blocks for integrative analysis [@Uchiyama:2019].

## Extending the BioLink Model

The BioLink Model is a data model developed for representing
biological and biomedical knowledge. It was designed with the goal of
standardizing the way information is represented in a graph store
regardless of the formalism used. The working group focused on
extending this model to support representation of a wide variety of
knowledge.

The following tasks were accomplished as part of BH19:

1) represent Datasets, and its related metadata
2) represent Family and Pedigree information, to support clinical knowledge
3) make the provenance model more rich and descriptive

For future work, the group will ensure that the new classes added to
the model will have appropriate mappings to other schemas and
ontologies.

##  Relational Biolink type inference for mediKanren

* Remote member Nada Amin, Chris Mungall, Deepak Unni, Will Byrd

* Goal: implement a relational type inferencer for the Biolink model in miniKanren, which can be integrated into mediKanren

* Nada added a `yaml` subdirectory to the mediKanren GitHub page, and created multiple files:

https://github.com/webyrd/mediKanren

** `yaml2sexp.py` generates the `biolink.scm` file, which contains an s-expression version of the Biolink yaml file

** `yaml.scm` contains miniKanren relations, and Chez Scheme code that generates miniKanren relations based on `biolink.scm` (basically these are giant `conde` clauses that can be though of as relational tables);  `yaml.scm` also contains tests for the relations.

Chris and Deepak are guiding us wrt the Biolink semantics

TODO

* integrate into the Racket mediKanren code

* integrate with the data categories in the KGs

* create query editor with decent type error messages, autocomplete, query synthesis, etc.

# Discussion

# References
