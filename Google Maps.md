# Google Maps System Design

## Functional Requirements:

* 1. Identify routes between source and destination
* 2. Suggest routes with respect to time and distance
* 3. Plugable design : There are not enough requirements initially. Then, design a pluggable system for requirements like traffic, weather and accident data to fit in later.


## Nonfunctional Requirements:

* 1. High Availability
* 2. Good Accuracy
* 3. Not too slow
* 4. Scale : 100 requests per hour (initially)


## Feasibility Constraints:
* 1. Data Set: Building a navigation application is a challenging problem. Not because of the kind of algorithms we use but more because of the kind of requirements it is associated with. If we try to calculate the number of roads in the world, there are roughly 100 million. Now, if we try to model it as a graph, we will have hundreds of millions of vertices and edges. This is a very massive dataset. This kind of information is non-existent.

* 2. Quantifying unpredictable attributes: It is tough to quantify the attributes that impact the ETA. With traffic, weather, road quality, road closure, and accidents, it is hard to develop a mathematical formula for ETA.


## Data Requirements: 
In the real world, for a system like Google Maps to work efficiently, vast amounts of data related to routes and roads are provided to Google by the government. Therefore, accepting the limitations and scope of the project, we will be using sample test routes to verify the system's performance.


## Algorithm analysis: 
* We will use the ideology of dynamic programming while we try to solve the problem. We will try to solve for the smaller and, later, for larger areas. A larger area is divided into smaller square segments. The idea behind these segments is that they will have four coordinates as vertices of the square to identify the segment boundary. Based on the segment boundaries, it is easy to determine whether a point lies inside the segment or not. We should map users with a segment based on the source location. As the segments are functions of latitude and longitude, we should be able to find the distance between the two segments. Firstly, we will solve the problem for one segment and later simulate the solution for larger areas with multiple segments.

* The way we model the road network is like a graph. In a road network, two weights are associated with an edge between two points - distance and time. The relationship between different points in the segment must be directional. The distance between two points will be the same, but the time taken concerning source and destination may vary.All the possible exits from a segment should be recorded as they form the connection to other segments. Graph algorithms like Dijkstra's or Bellman Ford can be used to find the single source shortest path graph for the given source and destinations. As an alternative, we can use the Floyd-Warshall algorithm to calculate the shortest path between all possible vertices, and once the results are calculated, we must cache them. 

* While calculating a suitable route between points across the segments, we need to consider the number of segments to go in each direction for exploration. This factor depends on the size of data set.


