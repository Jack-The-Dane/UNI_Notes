Dijkstra's Algorithm is a shortest-path algorithm used for finding the shortest path from a source node to all other nodes in a weighted graph. It is widely used in network routing and map navigation. ## How Dijkstra's Algorithm Works 
1. **Initialization**: - Start with a graph, where each node has a distance value initialized to infinity (`∞`), except the starting node which is set to 0. - Mark all nodes as unvisited. 
2. **Process the Current Node**: - For the current node, consider all of its unvisited neighbors. - Calculate their tentative distances by summing the current node's distance and the edge weight between the current node and its neighbors. - If the newly calculated tentative distance is smaller than the current distance value, update it. 
3. **Select the Next Node**: - After processing all neighbors of the current node, mark the current node as visited. A visited node will not be checked again. - Select the unvisited node with the smallest tentative distance and set it as the next "current node."
4. **Repeat**: - Repeat the process of processing nodes and selecting the next node until all nodes have been visited or the smallest tentative distance among the unvisited nodes is infinity (indicating that there is no reachable path). 
5. **Termination**: - The algorithm terminates when all nodes have been visited, and the shortest path to each node from the source is found. 
## Steps in Detail 
1. **Initialize**: - Let `dist[]` be the array of shortest distances from the source node to each node. Set `dist[source] = 0` and `dist[v] = ∞` for all other nodes `v`. - Create a priority queue (min-heap) to pick the node with the smallest distance. 
2. **Algorithm Execution**: - While the priority queue is not empty: - Extract the node with the minimum distance from the queue. - Update the distances of its unvisited neighbors. - If a neighbor's distance is updated, push it into the priority queue with the new distance. 
3. **Final Step**: - The algorithm will give you the shortest path from the source node to all other nodes. ## Example Given a graph:

## Time Complexity - 
**Time Complexity**: \( O(E \log V) \), where `E` is the number of edges and `V` is the number of vertices. The complexity arises from using a priority queue to select the minimum distance node. 
## Use Cases 
- **Network Routing**: Used to find the shortest path for data transmission in a network.
- **GPS Navigation**: Helps in finding the shortest route from the current location to a destination. 
- **Map Search**: Used in mapping applications to calculate the shortest route on a map.