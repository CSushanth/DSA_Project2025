# DSA_Project2025
1. Header Files & Constants

   These headers provide the required functionalities:
iostream for input/output,
fstream for file handling,
sstream (unused in current code but commonly used for string parsing),
map to store nodes,
string for string manipulation,
regex for pattern matching in code lines.

2.Data Structure - Node

Represents a line or block in code that is significant (e.g., if, while, for, etc.).
id: unique identifier for the node.
type: keyword representing type of code structure (if, while, etc.).
lineNum: original line number in the source file.
codeLine: actual code at that line.
connections[]: array of IDs that this node connects to (like a control flow).
connCount: number of valid entries in connections.
The constructor initializes the connections array with -1 and sets connCount = 0.

 3. Data Structure - Graph
Models a directed graph where each node represents a meaningful code construct.
Internally uses a std::map<int, Node> for storing nodes by ID.
Methods:
addNode(...)
Adds a new node with specified info.
addEdge(from, to)
Adds a connection from one node to another (directed edge), simulating control flow.
getTypes(...)
Extracts the type of each node into an array. Used later for similarity comparison.
printGraph()
Prints the entire graph in a human-readable format for debugging or analysis.

4. Function - makeGraphFromCode
Reads a file line by line and creates a graph based on code constructs.
Uses regular expressions to detect specific structures:
if(...)
while(...)
for(...)
Function definitions (simplified pattern)
return statements

5. Function - checkSimilarity
Compares two graphs based on the sequence of their node types.
Counts how many nodes of the same type appear in the same order (position-wise).
Returns a float value between 0.0 (no similarity) and 1.0 (identical).

6. Function - showMatchedParts

Goes through all nodes in both graphs.
Prints the first matching pair of nodes for each node in g1 (based on type).
Helpful for visualizing which parts of the code seem similar.

7. main() Function
Step-by-step:
Sets filenames: "file1.txt" and "file2.txt".
Calls makeGraphFromCode() to create two graphs.
Prints both graphs for visual inspection.
Calculates similarity score using checkSimilarity().
Prints a warning based on similarity score:
≥ 80% → likely copied.
50%–79% → somewhat similar.
< 50% → considered different.
Shows matching parts using showMatchedParts().

