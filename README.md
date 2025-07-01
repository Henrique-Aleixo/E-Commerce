# TFC - DEISI 64 - Recommender Systems

- Deisi64 (Analysis of joint purchasing patterns for recommendation systems in an online gift store), Copyright of Henrique Aleixo e João Serralha, Universidade Lusófona.

## **Presentation text**

A recomendação de produtos desempenha um papel vital no panorama do
comércio eletrónico atual. À medida que as lojas online continuam a crescer, este aspeto
torna-se um dos principais impulsionadores do sucesso e da competitividade no
mercado. No entanto, muitos sistemas de recomendação tradicionais enfrentam
desafios em termos de precisão e relevância das recomendações oferecidas. Portanto,
aprimorar a precisão das recomendações tornou-se um objetivo fundamental.
O nosso objetivo foi a aplicação de análise de redes sociais com intuito de
beneficiar os sistemas de recomendações numa gift store.

## **Presentation image**

![Shares2](assets/shares2.png)

___
## **Introduction**

The recommendation of products plays a vital role in the landscape of e-commerce. 
As online stores continue to grow, this aspect becomes one of the main drivers of success and competitiveness in the market. Therefore, enhancing the
accuracy of recommendations has become a fundamental goal.
With a view towards application in recommendation systems, in this Final
Coursework (TFC), we explore a dataset containing over 500,000 records of purchases
from a gift store. The intention is to use this data to create a network structure that
allows us to explore various network analysis methodologies. We aim to relate
products, purchases, and customers, extracting information from these relationships
to make more effective recommendations.

To carry out our Final Course Work we will use several disciplines and
scientific areas taught in the Computer Engineering course.[^ULHT21]

[^ULHT21]: Universidade Lusófona de Humanidades e Tecnologia, www.ulusofona.pt,
acedido em Out. 2021.

## **DataSet**

This is a transnational data set which contains all the transactions occurring between 01/12/2010 and 09/12/2011 
for a UK-based and registered non-store online retail.The company mainly sells unique all-occasion gifts. 
Many customers of the company are wholesalers.[^DataSet]

[^DataSet]: Online Retail. (2015). UCI Machine Learning Repository. https://archive.ics.uci.edu/dataset/352/online+retail

![OnlineRetail Banner](assets/OnlineRetail.png)

## **Installation guide**

To run the simulation, you need to pull the repository.
Then, install [Python environment](https://www.python.org/downloads/) and you will have two options:

Either open the the folder with [VSCode](https://code.visualstudio.com/download)

***OR***

Install [Jupyter Notebook](https://jupyter.org/install) to open the files locally.

## **Libraries**

Before running the queries, it is required to install these packages in the VSCode terminal

Package | Installation
 :---: | ---
`pip` | python get-pip.py
`openpyxl` | pip install openpyxl
`numpy` | pip install numpy
`networkx` | pip install networkx
`matplotlib` | pip install matplotlib
`pandas` | pip install pandas
`seaborn` | pip install seaborn
`scipy` | pip install scipy

***All done.*** Now, you can run the queries and make sure you have all the files locally.

## **Gephi**

To be able to create a network structure, it is required to use a open source platform called Gephi[^BaHe09]. This software has many important functions, but what we want
is to transform our input to something we can see graphically. It uses social network analysis algorithms for our purpose.

[^BaHe09]: Bastian M., Heymann S., Jacomy M. (2009). Gephi: an open source software for
exploring and manipulating networks. International AAAI Conference on Weblogs
and Social Media.

![Gephi](assets/gephi1.png)

## **Network creation process**

First, we need to check the data we have and take out information that we will not need, to be easier to make this process.
In this specific DataSet, we encountered cells that had products reimbursed, expenses from the store and some cells without
Client ID's, being this data to be filtered from the original DataSet.

![Filter](assets/filter.png)

### 1. **Product-Product Network**

The idea in this network, is that products frequently purchased together have some degree of similarity from the outset, therefore
if a user is buying product X, product Y and Z will be recommended if these are normally purchased together with X.

![Product Map](assets/product.png)

With the filtered dataset, we can start by grouping the data by **CustomerID** and **StockCode**. Next, let's put this together
table that we created with itself, with the Customer ID being the connection key.

![Merge](assets/merge.png)

With the relationship created we can now remove the repeated instances as per
example ‘A-A’. We will also give a ‘weight’ to each relationship taking into account the
number of occurrences of the same.

![Weight](assets/weight.png)

This data is inserted into a .csv file and imported to Gephi, where it uses a **Community Detection Algorithm**[^ViJe08] and gives us the __number of communities__ and a __similarity number__ (Modularity Class). Then, we use a distribution algorithm called **Force Atlas** to make the representation needed and added different
colors to each different community encoutered.

[^ViJe08]: Vincent D Blondel, Jean-Loup Guillaume, Renaud Lambiotte, Etienne Lefebvre, Fast unfolding of communities in large networks, 
in Journal of Statistical Mechanics: Theory and Experiment 2008 (10), P1000

![Network1](assets/network1.png)

Context | Statistics
 :---: | ---
`Number of nodes` | 2540
`Number of edges` | 96607
`Average Degree` | 76,069
`Number of Communities` | 22
`Modularity Class` | 0,230

Despite the number of communities, from this representation we can see **six communities** that are more relevant (the ones we can see):

- [x] Purple Community :purple_circle:
- [x] Green Community :green_circle:
- [x] Blue Community :large_blue_circle:
- [x] Black Community :black_circle:
- [x] Orange Community :orange_circle:
- [x] Red Community :red_circle:

### 2. **Client-Client Network**

The second type of interaction we will explore is the similarity between
users based on the products they purchase. For example, we have three
users, A, B and C, and we find that A and B purchased products identical to those of
user C then we can recommend to user C products that both others
users have purchased, as illustrated below. Additionally, products purchased
by A and C but not by B, may also be of interest to B.

![Client Map](assets/client.png)

The process of creating the relationship is the same and only difference is that the key used for this merge is **StockCode**.

![Network2](assets/network2.png)

Context | Statistics
 :---: | ---
`Number of nodes` | 1717
`Number of edges` | 275463
`Average Degree` | 320,865
`Number of Communities` | 5
`Modularity Class` | 0,162

## **Results**

From this point, we want to extract all of this information and explore different patterns in each network. 
In order to do that, we propose some questions that need an answer:

**Question 1** - *Which products are most frequently purchased together with
others? What is its value in terms of recommendation?*

The term ‘Product Share’ or ‘Together Purchase’ refers to how many times a
product is purchased together with other products. For example, if product A is
purchased together with 75 other different products out of a total of 100, this
means that the 'Product Share' of product A is 75%. In short, it is a measure
which shows the popularity of a product.    

The following histogram represents the distribution of gift store products
depending on your joint purchase value (on the scale 0.0 is 0% and 1.0 is 100%):

![Shares1](assets/shares1.png)

Products that have a product share greater than 0.4 or 40% are not only not useful but
their existence has a negative impact on network viewing.
This is because they have too many connections with other products, so they end up
adding additional connections makes it difficult to interpret the network without adding
benefits.

Since products above 40% joint purchase have this type
of negative characteristics for visualization, we decided to create a maximum threshold
of product share that a product can have. Any product above >40% of
joint purchase will be eliminated in order to reduce noise and therefore
improve network visualization and interpretation.

![Shares2](assets/shares2.png)

**Question 2** - *Which products are most frequently purchased together?*

In the generated network, we obtained a modularity value of 0.23, which is
considered suboptimal. This value indicates that the community structure present in the
network is not very strong, that is, connections within communities are not
significantly denser than connections between different communities.

In order to facilitate the understanding of the differences between the main communities
we obtained a Top 5 of the most popular products for each community, as can be seen
observe in this output.

![Products](assets/products.png)

Using this information along with manually searching for products by
communities we were able to identify the main themes in some communities:
+ Community 1 – bags and purses
+ Community 2 – kitchen utensils
+ Community 3 – gardening and outdoor tools
+ Community 4 – baking articles
+ Community 6 – Christmas objects and decorations

**Question 3** - *What are the Customer profiles?*

The following figure represents the Customer-Client network already changed in order to
enable better visualization. In the network, each node is a representative of a client and
the edges between the nodes represent the connection between two clients, that is, clients that
have purchased items in common. To obtain this visualization we had to
manipulate the initial network by changing the impact of certain parameters, e.g.
assign size to nodes depending on their degree.

![Clients](assets/client_modif.png)

The degree represents the number of other customers who also purchased
the same products as the initial customer. In other words, if a customer purchased
certain products, your node degree is determined by the number of customers that
purchased any of these same products.

![Degree](assets/node_degree.png)

As seen in this figure, we obtained the value 286 as the median. This means
that half of customers are connected to 286 or more other customers that
shared at least one product in common. This median reflects the distribution
of connections in the customer network, indicating that there is a large number of customers
with a considerable number of purchases in common.

## **Conclusion**

The main objective of this Final Course Work (TFC) was the investigation and
exploration of the records of an online gift store, with the aim of observing and
analyze joint purchasing patterns. Through the analysis of social networks we intended
understand how various types of network modeling impact the similarity between
products and customers and how we can use this to improve recommendations.

Through analysis we come across the results of the investigation, firstly
We want to refer to the level of modularity of the generated networks. As we already had
mentioned, this low level of modularity indicates that there is a weak structure of
communities, which makes certain types of analysis difficult for us since using the
communities for recommendations may not be effective.