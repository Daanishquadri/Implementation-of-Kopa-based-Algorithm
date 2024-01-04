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

Figure 1. The pseudo code for the k-means-based optimal path algorithm proposed by Desai et. al [1].

Once all of the CHs for each cluster are found and added to V, a new graph F is formed for the 	CHs. The source node CH is assigned to P and the destination node CH is assigned to Q. Distance M and N are then computed as follows:

<img width="255" alt="Screenshot 2024-01-04 at 3 16 32 PM" src="https://github.com/Daanishquadri/Implementation-of-Kopa-based-Algorithm/assets/84735952/31bcbc54-3ff1-432e-b098-7e7f02421116">

The algorithm then checks if the source node CH is the same as the destination node CH by checking if P is equal to Q. If P is equal to Q, then the communication distance between the source and destination nodes is M plus N. If the source node CH is different from the destination node CH, then the algorithm finds the optimal communication distance between the source node CH P and the destination node CH Q over the CH graph F using Dijkstra’s shortest path algorithm. This value is assigned to B and is subsequently added to M and N to give the optimal communication distance L.

The time complexity of the KOPA algorithm is given as

<img width="95" alt="Screenshot 2024-01-04 at 2 49 57 PM" src="https://github.com/Daanishquadri/Implementation-of-Kopa-based-Algorithm/assets/84735952/b2f307b1-b9e4-4035-8d37-40453358ad60">

where n is the number of nodes in the network, and K is the number of clusters.
The pseudo code for the next two algorithms are shown in Figures 2 and 3. They find the optimal communication length in different manners than KOPA, however they have a similar structure. The algorithm that we have chosen to base our implementation off of is the KOPA algorithm, which is why we have chosen to explain that one much more thoroughly than the others.

# 2.3 Performance of Algorithms

To measure the performance of this algorithm, the authors use common evaluators for the performance of SDN with IIoT. These markers include efficiency, round-trip time (RTT), throughput, and the total cycle time.

The efficiency of the routing algorithm, denoted by η, is dependent on transmission time, propagation delay, queuing delay, and processing delay. Figure 4 shows the comparison in η between five routing algorithms, COPA, MIOPA, KOPA, DSPA, and adaptive transmission power optimization (ATOP). The figure shows that KOPA falls short to COPA and MIOPA, however it outperforms the other traditional routing 



















