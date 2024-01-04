# Implementation-of-Kopa-based-Algorithm
Research Project on Implementation of Kopa based Algorithm

# Abstract
In the modern Industrial Internet of Things (IIoT), the efficiency of the network heavily relies on the ability for the machines to be able to find the shortest path of communication from one node to another. While traditional routing algorithms, such as Dijkstra’s shortest path algorithm (DSPA), are capable, there is room to improve the efficiency of routing algorithms within an IIoT environment. In this paper, we aim to implement a routing algorithm based on the k-means-based optimal routing algorithm (KOPA) that was proposed by Desai, Mini, and Tosh in their paper titled “Edge-Based Optimal Routing in SDN-Enabled Industrial Internet of Things”. The authors propose the KOPA which uses clustering to minimize the distance between nodes. In our implementation, we make use of Python as the programming language. We create a simple hypothetical network topology consisting of three clusters with arbitrary communication costs, and run our simplified version of KOPA against it. 


# 1 Introduction
In the world of manufacturing, new technologies like automation and digital changes have greatly improved on how the products are made. Smart manufacturing (SM) which is also known as industry 4.0, is all about using digital technology in manufacturing processes. It basically focuses not only on automating things but also making the development of products more efficient. This involves devices that can communicate with each other over the internet, which is known as the Industrial Internet Of Things (IIOT).

One important aspect of industry 4.0 is having a network which is easily programmable for communication. This is where the software defined networking which is also known as SDN comes into play. SDN separates the regular functions of a network into two parts to make it more flexible. In this article, we discuss creating a special kind of SDN routing algorithm that can adapt to the needs of an IIoT environment. 

Many industries, despite the rise of smart manufacturing, still face challenges in fully automating their processes. Traditional networks make this hard because they are not very flexible. SDN can be particularly useful in a scenario like the IIoT. SDN for IIoT, or SD-IIoT, uses SDNs to make networks programmable, increasing communication efficiency. 

This article explores how previous researchers have proposed SDN frameworks to improve communication efficiency within an IIoT environment. Traditional routing algorithms, such as Dijkstra’s shortest path algorithm, are staples in modern SDN architectures, however there are researchers who are proposing new and improved algorithms that provide a higher efficiency that those traditional algorithms.

# 2 Previous Work
In the article, “Edge-Based Optimal Routing in SDN-Enabled Industrial Internet of Things”, Desai, Mini, and Tosh discuss and emphasize the importance of routing algorithms in software-defined networking (SDN) environments, particularly their effect on the communication efficiency between machines within the industrial internet of things (IIoT) environment [1]. The authors break down every communicator within the IIoT network (machines, computers, etc.) into individual nodes that all together comprise the network topology. The challenge is to develop an architecture that will find the fastest and most efficient communication path between any two nodes.

# 2.1 Framework
To address this challenge, Desai et. al developed a system of representations and equations to give the optimal path of communications between any two nodes using clustering [1]. The network is modeled as a graph G composed of V and E, where V is the set of all nodes within the network and E is the set of all edges between these nodes. The graph G is reduced into K clusters, giving the set of cluster heads (CH) C. 

Given these sets, the optimal communication distance between two nodes is total of the distances from source node to source cluster head, source cluster head to destination cluster head, and destination cluster head to destination node. If the source and destination nodes are within the same cluster, then the optimal communication distance is simply the distance between source and destination nodes [1].

Mathematically, these distances are represented as:

<img width="145" alt="Screenshot 2024-01-04 at 3 09 57 PM" src="https://github.com/Daanishquadri/Implementation-of-Kopa-based-Algorithm/assets/84735952/100470bd-8c1e-4432-8548-19ed7f3c6c74">

where d is the optimal communication distance between source node and destination node, M is the minimum distance between source node and source cluster head, B is the minimum distance between source and destination cluster heads, and N is the minimum distance between destination cluster head and destination node.

These mathematical sets and equations are the basis for the representation of communication between nodes in a smart manufacturing (SM) environment. SM refers to the shift from traditional manufacturing methods to modern industrial automation and digital technologies within manufacturing industries [1]. SM environments utilize IIoT for their manufacturing processes.

Typically, the number of IIoT devices communicating within an SM environment is limited and established. Knowing the number and kinds of devices within a network allows the network engineers to understand the entire system, and test which routing algorithms are best suited to the network at hand. Routing algorithms are one of the largest constraints that conventional networks face, as they are directly related to the efficiency of communication between two nodes. Desai et. al understood all of these factors that affect the efficiency of network communication, and therefore have proposed a framework and algorithms for network engineers to implement within an SM environment [1]. These algorithms take advantage of the fact that SM networks typically have limited communicating nodes, but also include dynamic adaptability to include or exclude any nodes that are added or removed from the network. The handling of this dynamic network topology accounting is handled by the SDN controller, which also deploys whichever routing algorithm that the network engineer supplies to it.

# 2.2 Routing Algorithms
Desai et. al have proposed three different routing algorithms that leverage graph reduction and clustering to find the most optimal communication distance between two nodes. The authors abstract the actual machines and devices communicating into nodes, where each node within the network has equal priority over each other regardless of its location or communication information. The three algorithms that the authors propose are:

KOPA k-means-based optimal path algorithm for SDN framework

COPA cluster-based optimal path algorithm for SDN framework

MIOPA minimum interval-based optimal path algorithm for SDN framework

The first of these three algorithms, KOPA, is the routing algorithm that we have based our implementation off of. The pseudo code for this algorithm is shown in Figure 1. The algorithm takes three inputs, the source node (S), destination node (S), and number of clusters (K). Firstly, the algorithm reduces the network graph G into K clusters. For each cluster, the algorithm selects the node within the cluster that has the least euclidean distance between itself and the centroid of the cluster as the cluster head (CH), and adds it to a set of CHs, V. The euclidean distance between any two nodes, A(xa, ya), B(xb, yb) is given as 

<img width="232" alt="Screenshot 2024-01-04 at 2 48 17 PM" src="https://github.com/Daanishquadri/Implementation-of-Kopa-based-Algorithm/assets/84735952/075f4186-c6eb-4c3d-a5d3-9cc923379d20">

<img width="300" alt="Screenshot 2024-01-04 at 2 46 28 PM" src="https://github.com/Daanishquadri/Implementation-of-Kopa-based-Algorithm/assets/84735952/96beeb07-17fc-4189-bd6d-02fc6a8196d4">

Figure 1. The pseudo code for the k-means-based optimal path algorithm proposed by Desai et. al [1].

Once all of the CHs for each cluster are found and added to V, a new graph F is formed for the 	CHs. The source node CH is assigned to P and the destination node CH is assigned to Q. 

Distance M and N are then computed as follows:

<img width="232" alt="Screenshot 2024-01-04 at 2 48 17 PM" src="https://github.com/Daanishquadri/Implementation-of-Kopa-based-Algorithm/assets/84735952/c0e74431-d17b-4bb2-a055-1ac57506393c">

The algorithm then checks if the source node CH is the same as the destination node CH by checking if P is equal to Q. If P is equal to Q, then the communication distance between the source and destination nodes is M plus N. If the source node CH is different from the destination node CH, then the algorithm finds the optimal communication distance between the source node CH P and the destination node CH Q over the CH graph F using Dijkstra’s shortest path algorithm. This value is assigned to B and is subsequently added to M and N to give the optimal communication distance L.

The time complexity of the KOPA algorithm is given as :

<img width="95" alt="Screenshot 2024-01-04 at 2 49 57 PM" src="https://github.com/Daanishquadri/Implementation-of-Kopa-based-Algorithm/assets/84735952/06a74f35-d02c-417a-9c21-a51577592e02">

where n is the number of nodes in the network, and K is the number of clusters.
The pseudo code for the next two algorithms are shown in Figures 2 and 3. They find the optimal communication length in different manners than KOPA, however they have a similar structure. The algorithm that we have chosen to base our implementation off of is the KOPA algorithm, which is why we have chosen to explain that one much more thoroughly than the others.

# 2.3 Performance of Algorithms

To measure the performance of this algorithm, the authors use common evaluators for the performance of SDN with IIoT. These markers include efficiency, round-trip time (RTT), throughput, and the total cycle time.

The efficiency of the routing algorithm, denoted by η, is dependent on transmission time, propagation delay, queuing delay, and processing delay. Figure 4 shows the comparison in η between five routing algorithms, COPA, MIOPA, KOPA, DSPA, and adaptive transmission power optimization (ATOP). The figure shows that KOPA falls short to COPA and MIOPA, however it outperforms the other traditional routing algorithms. The proposed  KOPA algorithm has a higher efficiency than traditional routing algorithms such as DSPA and ATOP. 

<img width="302" alt="Screenshot 2024-01-04 at 2 51 46 PM" src="https://github.com/Daanishquadri/Implementation-of-Kopa-based-Algorithm/assets/84735952/e0c6eb00-3722-4324-874c-3d6032752602">

Figure 2. Pseudo code for the cluster-based optimal path algorithm proposed by Desai et. al [1].

The next attribute the authors evaluated was the algorithm’s throughput, which is calculated as the number of bits sent per second and denoted 

<img width="301" alt="Screenshot 2024-01-04 at 2 52 44 PM" src="https://github.com/Daanishquadri/Implementation-of-Kopa-based-Algorithm/assets/84735952/b6ef298a-8402-40a1-a001-d67ba3fb980b">

Figure 3. Pseudo code for the minimum interval-based optimal path algorithm proposed by Desai et. al [1].

as γ. Once again, KOPA landed right in the middle when compared to COPA, MIOPA, DSPA, and ATOP. Figure 5 shows the throughput performances of all the routing algorithms. The difference between KOPA, COPA, and MIOPA in throughput is nearly negligible as the data amount increases.

<img width="340" alt="Screenshot 2024-01-04 at 2 53 42 PM" src="https://github.com/Daanishquadri/Implementation-of-Kopa-based-Algorithm/assets/84735952/85df7bac-9c24-47ce-afa0-2ad6fe849d64">

Figure 5. Throughput of routing algorithms vs the data amount for n=100 [1].

The next measurement, RTT, depends on the transmission medium in which data is sent. For any medium, DSPA will always have the shortest RTT compared to COPA, KOPA, and MIOPA. When comparing the three algorithms on their own, KOPA has the shortest RTT of the three due to the tightness of its clusters. The RTT results prove that a balanced approach to resource utilization is required to obtain the optimal path for communication.

The final measurement the authors performed 

<img width="322" alt="Screenshot 2024-01-04 at 2 54 28 PM" src="https://github.com/Daanishquadri/Implementation-of-Kopa-based-Algorithm/assets/84735952/ab40792e-d0c8-4df5-b570-8508261ad661">

Figure 6. Total cycle time of routing algorithms versus the data amount for n=100 [1].

was total cycle time, which is the end-to-end time required for data transmission, denoted as ς. 

Once again, DSPA has the shortest total cycle time. MIOPA and KOPA are nearly indistinguishable, however. COPA performs slightly worse than both MIOPA and KOPA. Figure 6 shows the graph of total cycle time for all the algorithms.

From this research, it is evident that the routing algorithms proposed in this paper have better efficiency and throughput than traditional routing algorithms such as DSPA. Despite having longer RTT and total cycle times compared to DSPA, the algorithms are less computationally expensive.

Given this prior research, we decided to implement a version of KOPA to prove that an actual implementation of this algorithm is feasible.

# 3 Implementation

The algorithm that we aim to implement is not a one-to-one replication of the KOPA algorithm proposed by Desai et. al. Given the unavailability of an IIoT for us to implement and test our algorithm on, we will be using an abstracted hypothetical network topology to test our algorithm on. We will assume that the network will have already been separated into clusters, with cluster heads already chosen and distances between nodes already defined with an edge weight. This negates the need for our KOPA-based algorithm to separate the network into clusters, calculate the physical distances between nodes, and choose cluster heads based on the euclidean distance between each node and the centroid of each cluster.

With these differences understood, the algorithm we plan to implement will use our implementation of Dijkstra’s shortest path algorithm to find three paths; the shortest path from source to source cluster head, the shortest path from source cluster head to destination cluster head, and finally the shortest path from destination cluster head to the destination node. The sum of these path costs will give the shortest communication distance from the source node to the destination node under a similar set of processes as the proposed KOPA algorithm. 

An added feature that our implementation has is the ability to record the actual path that the communication must follow to achieve the shortest communication distance. The proposed KOPA algorithm only records the distance, not the actual path that the communication must take place on.

The implementation of our algorithm will be done in Python.

# 3.1 Hypothetical Network Design

As stated previously, the network we will be using our algorithm on will already have each cluster pre-defined and distance costs defined for each node within each cluster. Nodes within a cluster are only allowed to communicate with other nodes within that same cluster. Only the cluster heads from each cluster will be able to communicate with each other outside of their cluster.


<img width="348" alt="Screenshot 2024-01-04 at 2 58 04 PM" src="https://github.com/Daanishquadri/Implementation-of-Kopa-based-Algorithm/assets/84735952/6a855fa0-e800-404e-9d26-2d8a41c2495f">

The network topology is quite arbitrary, so we decided on a network consisting of fourteen unique nodes, denoted as letters from A to N, divided into three clusters. The first cluster consists of five nodes, A to E, where B is the cluster head. The second cluster consists of four nodes, F to I, with F as the cluster head. The final cluster consists of five nodes, J to N, with J as the cluster head. The complete topology is shown in Figure 7.

The communication between cluster heads is represented again as a cluster in Figure 8. These nodes are all able to communicate with each other and have pre-defined communication distances.

The network topology is defined as a list of dictionaries in the code. The topology list contains the various clusters and is passed into the algorithm as an argument. An example of a cluster defined in a dictionary is as follows:

cluster_b = {
'A': {'B': 2, 'C': 3, 'E': 4},
'B': {'A': 2, 'E': 3},
'C': {'A': 3, 'E': 1, 'D': 5},
'D': {'C': 5},
'E': {'A': 4, 'B': 3, 'C': 1}
}

The keys are the different nodes within the cluster. The following dictionary assigned to each node contains the distances from that node to the other nodes that it has direct communication with. The nodes with which the key node does not have direct communication with are omitted.

# 3.2 DSPA

The first part of our implementation is the Dijkstra’s shortest path algorithm (DSPA), which is what our KOPA implementation will rely on. We implemented this algorithm from the ground up, following the steps taken in DSPA.

<img width="348" alt="Screenshot 2024-01-04 at 2 58 04 PM" src="https://github.com/Daanishquadri/Implementation-of-Kopa-based-Algorithm/assets/84735952/9d39af83-6bc8-4c7e-aa20-7e916a19724e">

The DSPA function takes in three parameters, the source node, destination node, and cluster.

The algorithm first creates a dictionary that sets the distances for each node to infinity, except for the distance between the source node and itself, which is set to zero. The algorithm also creates a priority queue list to keep track of the node with the minimum distance, as well as a predecessor dictionary to keep track of the path taken from source node to destination. The lists and dictionaries are as follows:

distances a dictionary to keep track of all the distances between all of the nodes in the graph

priority a list to keep track of all the minimum distances for each node

predecessors a dictionary to keep track of the path taken to each node

The algorithm starts with the source node and temporarily stores its current distance. It then checks to see if the current distance is different from the recorded distance. If it is greater, it ignores that node and goes to the next one. If it is less, the algorithm will find the node in the graph and temporarily add the distance to its neighbors to the current distance. If this distance is shorter than the straight path to its neighbor, it will update the distances dictionary as well as the predecessors dictionary.

To find the path along the shortest distance, the algorithm goes through the predecessors dictionary and adds each node along the path until it reaches the destination node.
The code for the DSPA function can be found at the link in the availability section at the bottom of this paper.

# 3.3 KOPA-based Algorithm

The KOPA-based algorithm that we have implemented takes three parameters which are similar to the parameters for the DSPA function, source node, destination node, and complete network topology which is given as a list of clusters. The last cluster in the topology list must be the cluster head cluster.

The algorithm first initializes four variables:

length an integer that represents the shortest distance between source node and destination node

source_cluster a dictionary that holds the cluster that contains the source node

dest_cluster a dictionary that holds the cluster that contains the destination node

ch_cluster a dictionary that holds the cluster head cluster

The algorithm first finds which clusters hold the source and destination nodes by iterating through the list of clusters that was passed through as a parameter. If the given source node is in the current cluster, then the source_cluster variable is assigned to that current cluster. The same goes for the dest_cluster variable.

The algorithm then checks to see if the source and destination node are in the same cluster. If they are, then the function calls the DSPA with the source cluster, source node, and destination node as inputs. The output of that DSPA call is the shortest path and distance for the source and destination node, so our algorithm will return those values.

If the source and destination nodes are in different clusters, the algorithm will continue on and find the cluster heads for both the source and destination cluster. The algorithm does this by comparing each node in the source and destination cluster to the keys in the cluster head cluster. The keys that match are the cluster heads for the source or destination cluster.

Once this information is gathered, the algorithm makes three calls to the DSPA function. The first call is to get the shortest path from the source node to the source cluster head and it returns the distance between the two along with the path along that distance. The same is done for the destination cluster head and destination node, as well as with the source cluster head and destination cluster. The output of these three calls to DSPA give us the distance and path between: source node and source cluster head, source cluster head and destination cluster head, and destination cluster head and destination node. The code to call these functions is given here:

<img width="258" alt="Screenshot 2024-01-04 at 3 01 07 PM" src="https://github.com/Daanishquadri/Implementation-of-Kopa-based-Algorithm/assets/84735952/719e0ba1-824e-405a-a80e-ddeb17c8f7f6">

The final length and path is given as the sum of all of the distances and paths from the previous DSPA calls. The function returns these sums as the result of the algorithm:

sc_path.pop()
ch_path.pop()

length = sc_dist + ch_dist + dc_dist
path = sc_path + ch_path + dc_path
return path, length

It is necessary to remove the last element of the first two path lists, as leaving them in would result in duplicate nodes being on the path. 

The final output is formatted as such:

path, distance = kopa(topology, start_node, end_node)
print(f'The optimal communication distance between {start_node} and {end_node} is {distance} over the path: {path}')

# 4 Results

To test our algorithm, we simply need to pass in variables to the algorithm. Knowing the entire network topology, we arbitrarily select two nodes, C and H, and manually determine the distance and path between them. Looking at figures 7 and 8, we can see that the optimal path between C and H, passing through the cluster heads, is C - E - B - J - F - G - H and the distance would be twelve.

We can pass these parameters to algorithm with following code:

topology = [cluster_b, cluster_f, cluster_j, clusterheads]
start_node = 'C'
end_node = 'H'
path, distance = kopa(topology, start_node, end_node)

To run the program, we move to the programs directory in our terminal, and run the command py kopa.py. The program returns the following output:

The optimal communication distance between C and H is 12 over the path: ['C', 'E', 'B', 'J', 'F', 'G', 'H']

As we can see, the algorithm produces the exact results we expected it to. To test it in a different case, we can choose two nodes from the same cluster, A and D. We expect the output to be eight, along the path A - C - D. Running the program with these two nodes as the inputs, we get the output:

The optimal communication distance between A and D is 8 over the path: ['A', 'C', 'D']

The algorithm will work for any two nodes selected from the network topology.

# 5 Conclusion

In conclusion, combining IIoT with edge based optimal routing greatly improves how things work in smart manufacturing. Using SDN also makes communication between devices in this setup much better.

In this paper, we discussed three new algorithms to the communication route within a network, proposed by Desai et. al: KOPA, COPA, and MIOPA. Experimental results proved these methods work better and faster than the usual DSPA when used in the SDN framework. All three algorithms are quicker because they use smart techniques such as clustering to simplify network topology.

Although DSPA performs well in terms of total cycle time and Round-Trip time, it needs more computer power. In practical terms, KOPA, COPA, and MIOPA are more useful for SM. The idea of looking at different factors like distance, bandwidth, and smart simplification through clustering shows that choosing KOPA, COPA, or MIOPA makes sense for SM.

To add to this research, we decided to implement a prototypical version of the KOPA algorithm in Python that finds the optimal communication path and distance for a theoretical network topology. We have made a few assumptions in our prototype, such as pre-determined clusters and cluster heads. Our implementation shows the feasibility of implementing the KOPA algorithm in an SDN environment, and using it to find the optimal communication distance, as well as the optimal communication path, between any two nodes within the network.

Further research could include making these algorithms even better by adding ways to balance the load and create multiple paths for data transmission if the best path is too crowded. Researchers could also implement these algorithms in a real life IIoT environment and test the performance against traditional routing algorithms. Our research shows the feasibility of implementing such algorithms, and further research could increase the communication efficiency dramatically in SM environments.

# Availability
The source code for our algorithm can be found at this GitHub 





















