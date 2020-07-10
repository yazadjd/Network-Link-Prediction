# Network-Link-Prediction

### Overview
Pairwise relationships are prevalent in real life. For example, friendships between people, communication links between
computers and pairwise similarity of images. Networks provide a way to represent a group of relationships.
The entities in question are represented as network nodes and the pairwise relations as edges.
In real network data, there are often missing edges between nodes. This can be due to a bug or deficiency in
the data collection process, a lack of resources to collect all pairwise relations or simply there is uncertainty about
those relationships. Analysis performed on incomplete networks with missing edges can bias the final output, e.g.,
if we want to find the shortest path between two cities in a road network, but we are missing information of major
highways between these cities, then no algorithmwill able to find this actual shortest path.
Furthermore, we might want to predict if an edge will form between two nodes in the future. For example, in disease
transmission networks, if health authorities determine a high likelihood of a transmission edge forming between
an infected and uninfected person, then the authorities might wish to vaccinate the uninfected person.
In this way, being able to predict (and correct for)missing edges is an important task.

### Task

In this project, we will be learning from a training network and trying to predict whether edges exist among test node
pairs.
The training network is a fragment of the academic co-authorship graph. The nodes in the network—authors—
have been given randomly assigned IDs, and an undirected edge between node A and B represents that authors A and
B have published a paper together as co-authors. The training network is a subgraph of the entire network, focussing
on individuals in a specific academic subcommunity.
The test data is a list of 2,000 edges, and the task is to predict if each of those test edges are really edges in the
authorship network or are fake ones. 1,000 of these test edges are real and withheld from the training network, while
the other 1,000 do not actually exist.

### Data Format

All data will be available in raw text. The training graph data will be given in a (tab delimited) edge list format, where
each row represents a node and its neighbours.

In addition to the edges, we are also provided with a file including several features of the nodes (authors). This
file, “nodes.json” is in JSON format and includes for each author:
- their id in the graph
- the number of years since their first and last publication
- their number of publications in total, num_papers
- presence of specific keywords in the titles and abstracts of their publications (denoted keyword_X where X 2 {0,1, . . . ,52}, each being a binary value and only listed if its value is 1)
- publication at specific venues (denoted venue_X where X 2 {0,1, . . . ,347}, each being a binary value and only listed if its value is 1)
This gives some additional information beside the network structure for your prediction task.

The test edge set is in a comma separated values (CSV) edge list format, which includes a one line header, followed
by a line for each (source node, target node) edge. The implemented algorithm should take the test CSV file as input
and return a 2,001 row CSV file that has 
- in the first row, the string “Id,Predicted”;
- in all subsequent rows, a consecutive integer ID, a comma, then a float in the range [0,1]. 
These floats are your “guesses” or predictions as to
whether the corresponding test edge was from the co-authorship network or not. Higher predictions correspond to
being more confident that the edge is real.

The test set will be used to generate an AUC for your performance. During the Kaggle competition, AUC on a 30% subset of the test set will be used to rank you
in the public leaderboard and the complete test set will be used to determine your final AUC and ranking.

### Files

The Data directory contains the required data files.

There are two python files that correspond to the source code
of the two different approaches followed. The code is in Python 3 programming language.

Logistic_Regression_Approach.py:

The first one is the Logistic_Regression_Approach.ipynb that contains code blocks
that perform network link prediction using a logistic regression machine learning
model. The code contains two sections and different functions that extract the 
positive and negative samples and uses features to train the model. Almost every 
code block contains comments to enhance understanding and readability. The dependencies
are the following python modules: pandas, numpy, csv, random, networkx, sklearn and
operator modules. The program can be run by simply runnning each block of code in order 
of the code blocks.


Node2Vec_Approach.py:

This notebook contains code blocks that perform network link prediction using the 
node2vec model and can be run by simply running each code block in the given order.
The dependencies are: pandas, numpy, csv, networkx and node2vec modules in python.
Comments are provided to enhance understanding and readability.

Both programs assume that the training data (train.txt), features data (nodes.json)
and the test data (test-public.csv) are in the current working directory.
The output file created is "pred.csv" in the required csv format that contains the
predictions.

The Report contains an Analysis of the approaches used explaining the results obtained.
