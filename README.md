# routing_assignment
Distance Vector Routing Algorithm
This project implements the Distance Vector (DV) routing algorithm (Bellman-Ford) for a network topology represented as an undirected graph. It calculates distance tables for each router at each iteration until convergence. It also supports topology updates (adding, modifying, or removing links) and recomputes tables. The bonus part implements Poisoned Reverse to prevent routing loops.
Features

Computes distance tables and routing tables for each router.
Handles topology updates (link addition, modification, removal).
Implements Poisoned Reverse (PoisonReverse.py) to prevent routing loops.
Outputs in the format specified by the assignment (#START, #INITIAL, #UPDATE, #FINAL).
Processes routers in alphabetical order and selects first best route alphabetically by next-hop.

To Do

 Add comments
 Add more test cases
 Implement split horizon
 Put classes in separate files
 Implement update section
 Implement routing table
 Implement convergence check
 Implement Distance Vector Routing algorithm
 Create distance table data structure
 Implement graph adjacency list
 Implement Poisoned Reverse

Usage
Run the programs with input redirected from a file:
./DistanceVector.py < input.txt
./PoisonReverse.py < input-update.txt

Input Format

List router names, one per line, ended by DISTANCEVECTOR:

X
Y
Z
DISTANCEVECTOR


List edges with weights (node1 node2 weight), ended by UPDATE:

X Z 8
X Y 2
Y Z 3
UPDATE


List updates (node1 node2 weight; -1 to remove), ended by END:

Y Z -1
X Z 3
END

Note: Updates are optional; enter END after UPDATE to skip.
Quick Start
Test with provided inputs:
./DistanceVector.py < input.txt > output.txt
./PoisonReverse.py < input-update.txt > output-pr.txt

Output Format

Distance tables at each step (e.g., X Distance Table at t=0).
Routing tables after convergence (e.g., Y,Y,2).
Sections: #START, #INITIAL, #UPDATE, #FINAL.
Update messages: t=n distance from X to Y via Z is d.

Example output (from input-update.txt):
#START
X Distance Table at t=0
     Y    Z
Y    2    INF
Z    INF  8
...
#INITIAL
X Routing Table:
Y,Y,2
Z,Y,5
...
#UPDATE
t=3 distance from X to Z via Z is 3
...
#FINAL
X Routing Table:
Y,Y,2
Z,Z,3
...

Files

DistanceVector.py: Main DV implementation.
PoisonReverse.py: DV with Poisoned Reverse.
Router.py: Router class for distance and routing tables.
Graph.py: Graph class for network topology.
input.txt: Sample input (no updates).
input-update.txt: Sample input with updates.
test-single-node.txt: Test case for single node.
test-disconnected.txt: Test case for disconnected network.
test-ring.txt: Test case for ring topology.
sample_topology_expected.txt: Expected output for reference.

Classes
Graph

add_edge(node1, node2, weight): Add undirected edge.
remove_edge(node1, node2): Remove edge.
get_neighbors(node): Get neighbors and weights.
print_graph(): Print adjacency list (debugging).

Router

initialize_distance_table(nodes): Initialize distance table.
print_distance_table(t): Print distance table.
update_self(graph, routers_list): Update with direct link costs.
send_updates(neighbors, routers_list, t, poisoned_reverse): Send updates, optionally with Poisoned Reverse.
process_received_tables(t): Process neighbor updates.
find_min_cost(distance_table, dest): Find minimum cost and next hop.
create_routing_table(): Create routing table.
print_routing_table(): Print routing table.
process_after_update(graph, routers_list): Process topology updates.
print_updates(): Print updates (debugging).


