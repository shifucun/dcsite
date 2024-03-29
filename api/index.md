---
layout: default
title: API
nav_order: 2
has_children: true
---
# Overview

[Data Commons](https://datacommons.org) is an open knowledge graph that
aggregates data from many different [data sources](https://datacommons.org/datasets)
into a single knowledge graph. Data Commons is based on the data model <link> used by [schema.org](https://schema.org).
Data Commons uses the Schema.org [data model](https://schema.org/docs/datamodel.html) and schema.

The **Data Commons API** is a set of APIs that allow developers to
programmatically access the data in the Data Commons graph. This access is
provided through a set of REST APIs, with additional wrappers in Python and R.

Our APIs can be roughly grouped into the following:

-   **Local Node Exploration**: Given a node (or set of nodes), explore the
    graph around those node(s).

-   **Domain specific APIs**: These are groups of APIs, specific to particular
    domains, E.g., places, statistics.

-   **Graph Query/SPARQL**: Given a subgraph where some of the nodes are
    variables, retrieve possible matches. This corresponds to a subset of the
    graph query language [SPARQL](https://www.w3.org/TR/rdf-sparql-query/).

-   **Utilities**: These are Python Notebook specific APIs for helping with
    Pandas DataFrames, etc.

For each API, in addition to the arguments and return value for the REST calls,
we also document language specific bindings.

Almost all our APIs take references to nodes and properties as arguments. Every
node (properties are also nodes) has a `Data Commons ID (DCID)`, which is used
to pass nodes as arguments to API calls. The DCID of schema.org terms used in
Data Commons is their schema.org ID.


<!--- TODO: update Setup section link --->
Using the Data Commons API requires an API Key. Details on obtaining a key,
installing Python libraries, etc. can be found in the Setup section.

<!--- TODO: update all the links below after pushing to github --->

### Local Node Exploration

-   **get_properties**: given a node, return the `DCID`s of the properties
    associated with this node. In graph terminology, return the `DCID`s of the
    arc-labels of the arcs into and out of this node.

    -   Documentation: **[REST](https://datacommons.org)**

-   **get_property_values**: given a node and a property, return the value of
    this property for that node. In graph terminology, return the target/source
    of the arcs into/out of this node with that arc label.

    -   Documentation: **[REST](https://datacommons.org)**

-   **get_triples**: given a node, return all the triples in which this node is
    either the subject/source or object/target.

    -   Documentation: **[REST](https://datacommons.org)**

### Graph Query/SPARQL

-   **query**: query DataCommons via SPARQL.

    -   Documentation: **[REST](https://datacommons.org)**

### Domain Specific APIs

#### Statistics

A substantial amount of the data in Data Commons is statistical in nature. The
representation of this information uses the concept of an
[StatisticalPopulation](https://browser.datacommons.org/kg?dcid=StatisticalPopulation)
with [Observation](https://browser.datacommons.org/kg?dcid=Observation)s on
these populations.

-   **get population**: given a list of place DCIDs, return the DCID of
    `StatisticalPopulation`s for these places, constrained by the given property
    values.

    -   Documentation: **[REST](https://datacommons.org)**

-   **get observation**: given a list of `StatisticalPopulation` DCIDs, return
    the DCID of `Observation`s for these statistical populations, constrained by
    the given observations' property values.

    -   Documentation: **[REST](https://datacommons.org)**

-   **get population and observation**: given the DCID of a node, return all the
    `StatisticalPopulation`s and `Observation`s for this node.

    -   Documentation: **[REST](https://datacommons.org)**

-   **get place observation**: return all `Observation`s for all `Place`s of a
    certain type, for a given `observationDate`, given a set of constraints on
    the `StatisticalPopulation`.

    -   Documentation: **[REST](https://datacommons.org)**

#### Locations

Many applications need listings of places of a given type, often within
containing areas.

-   **get place in place**: given a list of `Place` DCIDs (e.g. `County`,
    `State`, `Country`, etc...), return the DCIDs of places contained within, of
    a specified type.

    -   Documentation: **[REST](https://datacommons.org)**

