In Network Analysis we are often interested in finding "communities" embedded within larger networks. If, for example, our network is a social graph (perhaps extracted from a social networking platform) then the communities could represent well-connected groups of individuals who converse frequently with one another.

Community Detection algorithms are used to partition graphs into communities, and there are lots of them. (See https://cdlib.readthedocs.io/en/latest/reference/cd_algorithms/node_clustering.html for some examples.)

Two things have always bothered me about community detection algorithms. Firstly, when an algorithm paritions a graph into communities it is often difficult to explain exactly what defines them to a normal human. Even though many community detection algorithms (for example the Louvain Method) are based on well-defined metrics like modularity maximisation (informally the modularity of a partition can be described as the ratio of intra-community edges to intra-community edges), the explanation is confusing. It would be great to have an algorithm where the definition of a community is easily interprable.

The algorithm in this notebook does just that; a community is a collection of nodes who have a surprising number of neighbours in common.

The second thing that bothers me is that, in much of my work, I have been looking for partial partitionings of the graph. In a real-world social network it is often the case that large numbers of the nodes do not really belong to a "community" - they are peripheral and only weakly connected - whereas others are clearly part of well-defined groups, embedded within the graph. I want an algorithm to return me only those well-defined groups and leave the rest alone. The algorithm in this notebook does just that.

This notebook is a work in progress. I don't usually publish or share work in its early stages like this but I think the approach is somewhat unique (at least as far as my research suggests). There may well be better ways to address the two motivating problems above.

The (partially completed) algorithm is an attempt to derive and implement a principled algorithm for clustering an undirected, unweighted graph (though it could be extended to the directed or weighted case). It's working name is Similarity Clustering. Key features are:

    A "community" is defined as a set of nodes whose internal connectivity has an intuitive, probabilistic interpretation. Communities are defined as subgraphs where the probability of seeing so many interconnections between the nodes is sufficiently surprising that we reject a null hypothesis (that their connectivity is similar to the background connectivity of the wider graph).

    Not every node needs to belong to a community. Think of this approach as analagous to that of an unsupervised clustering algorithm like HBCScan.

    It's very simple to code and fast to execute.
