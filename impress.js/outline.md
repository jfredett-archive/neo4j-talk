 Graph DBs in General

* Polyglot / Roles for Graphs
  
  - Static RO

    * Allows you to be agressive in indexing

    * Good when storage is easier in another methodology (Documents/Relational)
        but query is easier in a graph format (ie, you're not querying much while
        producing, but heavy, complex queries while consuming)
      
      - Ex: Geneology + Artifact Catalog

      - Ex: Comic Book Chronology and Character Catalog

      - Ex: Online Store (Author new product pages w/ Document backend,
          display with "Related Items" via graph query for nearby edges)


  - Main Store

    * Natural model of data 

    * Schemaless, rapid prototyping

    * Useful for Social Networks, On-the-fly cataloging of data. Anything which
        rapidly evolving relationships between models

* Why Graphs?

  - Low ORM/Impedence. 

  - Natural model of many domains

  - Graph Metrics are meaningful in many applications (Centrality, Eccentricity, Diameter, Radius)

  - Deep questions are easy to ask (eg "How are these two things related"
      becomes, "What are the paths between these items")

* Graph Theory in small order

  - A Graph is a set of Nodes and Groupings of Nodes, called "Edges".

  - Typically an edge is a pair of nodes

  - Graph Theory is the study of graphs

  - Graphs model many hard problems in math and computer science.

  - They are good at describing complicated relationships (Ramsey Theory, Cliques)

#Neo4j

* How to install from scratch
  - Webadmin
    * Dashboard has some metrics (node count, edge count, property count, etc) and a chart

    * Data browser useful to look up individual nodes -- can also use the
        reference node, if you have one (it's easy to delete)

    * Console allows for Cypher, Gremlin, and HTTP queries to be executed
        against the DB

      Note that sometimes querys appear to take longer than claimed by the timer
      result, this is overhead due to rendering stuff on the screen!

    * Server info - lots of configuration stuff and java package names.

    * Index Manager - lists all the indicies, big buttons to delete them, not
        much else.

  - Language Libs

    * Embedded Install
      - Normal use case for dev
      - neo4j lives in ./neo4j/, data lives in ./neo4j/data/graph.db 
      - <brians instructions>

    * Server Install
      - Use your systems package manager / best installation practices 

    * Ruby
      - Use Neography
      - Psych/Syck + HTTParty + ECMA/RFC JSON
        * https://groups.google.com/forum/?fromgroups#!topic/neo4j/fdbsUNJWV4A 
      
    * Node
      - Install like the Embedded Install
      - do `npm install neo4j`

* Loading Data
  - graph.db copy to embedded install

    Pull from the local network, unzip in the './neo4j/data/graph.db' directory
      of your app

* Using Neo4j
  - Hosting
    * Heroku
      - Public Beta!
      - 256MB of storage available.
      - No easy way to clean the DB, use a gremlin query `g.clear()` to remove
          most of the stuff

  - Querying
    * Indicies
      - It _is_ an index
        Every Node is an index of the nodes it's connected to. 

        Traversers, cypher, and gremlin are like index queries

      - Lucene / "Normal" indicies

        Like more normal indicies

        Manually maintained (unless you use autoindexing, then certain
        properties will be indexed automatically)

        Useful for starting queries

        Works like a key-value store, with some full-text-search capability on
        the values

            eg: 

                start n=node:my_index("key_foo:something*")
                return n

        returns all the nodes that match that query on the index

      - Good indexing:
          Semantic Indexing in the graph

          Convienent indexing in "Normal Indicies"

          That is, if you have a graph of comic books, publishers, characters,
          and superpowers. Represent comic book genres with a "normal" index,
          and represent superpowers with real nodes. This makes sure that
          relationship queries don't find "Junky" paths that just find that, for
          instance, two nodes share a publisher who crossed genres.

          Downside to not representing "convienence" traits as nodes -- asking
          what genres a publisher created becomes more difficult

    * Cypher
      
      - SQL-y / SPARQL-y declarative query DSL

      - Alternative to Traversers or Gremlin

      - Basics:

        start <var>=<node|rel>(<id>)
        match <query>
        where <predicates>
        return <results>


    * Traversers, Gremlin, and BlueprintsAPI
    
      - Traversers start a node and span outward
      - Use specially configured values to specify path pruning, depth limits,
        etc
      - Sort of like (in fact, almost exactly like) a map/reduce, but with
        knowledge of the graph structure

      - Gremlin is a dataflow language in Groovy
      - Has a notion of "piping" like *nix shell.
      - aggregate many small tools to process data
      - more terse than Cypher -- far less readable.

* Visualization 
  - d3.js
  - neovigator



