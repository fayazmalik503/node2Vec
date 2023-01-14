Knowledge graph analysis with node2vec

We use CareerVillage knowledge graph analysis with node embeddings

1. Introduction
a.) What is a knowledge graph?
It is a network that represents multiple types of entities (nodes) and relations (edges) in the same graph. Each link of the network represents an (entity,relation,value) triplet. For example I give you some examples from the small knowledge graph below:

Eiffel Tower (entity) is located in (relation) in Paris (value)
Paris (entity) is an instance of (relation) city (value)
Alice (entity) is an instance of (relation) person (value)

The CareerVillage data set contains several different entities (persons, groups, schools, locations etc.). Thus one possible approach to analyse this data is to build a large knowledge graph representing as many relations as possible.

b.) What are node embeddings?
Embeddings, especially word representations (e.g. Word2Vec), is a hot research topic nowadays. The basic idea behind node embedding algorithms (e.g. node2vec, Line, DeepWalk etc.) is that if you generate node sequences originating from a given vertex and feed them to Word2Vec (like sentences from a text) you can map the nodes of the network into a low dimensional vector space. Usually these methods are optimized for the criteria to preserve the global/local role of each vertex in the graph.



CareerVillage knowledge graph analysis with node embeddings
1. Introduction
a.) What is a knowledge graph?
It is a network that represents multiple types of entities (nodes) and relations (edges) in the same graph. Each link of the network represents an (entity,relation,value) triplet. For example I give you some examples from the small knowledge graph below:

Eiffel Tower (entity) is located in (relation) in Paris (value)
Paris (entity) is an instance of (relation) city (value)
Alice (entity) is an instance of (relation) person (value)
Example knowledge graph

The CareerVillage data set contains several different entities (persons, groups, schools, locations etc.). Thus one possible approach to analyse this data is to build a large knowledge graph representing as many relations as possible.

b.) What are node embeddings?
Embeddings, especially word representations (e.g. Word2Vec), is a hot research topic nowadays. The basic idea behind node embedding algorithms (e.g. node2vec, Line, DeepWalk etc.) is that if you generate node sequences originating from a given vertex and feed them to Word2Vec (like sentences from a text) you can map the nodes of the network into a low dimensional vector space. Usually these methods are optimized for the criteria to preserve the global/local role of each vertex in the graph.

Example node embeding

c.) My work
In this work I use the node2vec algorithm to generate low dimensional representation for CareerVillage users based on the knowledge graph that I extracted from the data. My ultimate goal is to discover interesting user groups / clusters (e.g. popular professionals, satisfied students etc.) using only the available network structure..


2. Load data


3. Build knowledge graph from CareerVillage data


i.) Nodes
The vertices of the knowledge graph consists of the following entities:

answers
questions
comments
students
professionals
industries
schools
tags
user groups
group types

ii.) Edges


iii.) Location information
Location information of users and professionals are preprocessed before I add it to the knowledge graph. I tried to extract city / state / country hierarchy from locations were it was provided. In this case I created different levels for locations: cities, states/regions and countries.


4. Node2Vec

#First we generate random walks starting from each node of the knowledge graph by initializing the Node2Vec object
#Then we optimize node representations with the fit() method


Transition probability?
The probability of moving from one state of a system into another state. If a Markov chain is in state i, the transition probability, pij, is the probability of going into state j at the next time step.

What is transition probability in Markov chain?
The one-step transition probability is the probability of transitioning from one state to another in a single step. The Markov chain is said to be time homogeneous if the transition probabilities from one state to another are independent of time index

5. Visualization of node embeddings

I trained Node2Vec to map every node of the knowledge graph into a 10 dimensional Euclidean space. In order to visualize the results in 2 dimension I applied the t-SNE dimensionality reduction algorithm.


a.) User embeddings with t-SNE dimensionality reduction

I visualize only a randomly selected 50% of the users for clarity

6. Summary
The CareerVillage data contains several entities and different type of connections between them. My ultimate goal was to analyze this data only from the aspect of network structure.

I managed to separate the users into students and professionals using only the underlying knowledge graph. First I mapped the nodes of the network to the 10 dimensional Euclidean space with node2vec. Then I applied t-SNE dimensionality reduction to visualize the results.

