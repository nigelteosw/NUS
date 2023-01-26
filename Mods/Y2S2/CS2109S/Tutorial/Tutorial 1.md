# Problem Formulation & Uninformed Search

### 1. Determine the following environment properties of a Sudoku game
- Fully Observable
- Single Agent
- Deterministic
- Episodic
- Static 
- Discrete


### 2. Determine the PEAS (Performance measure, Environment, Actuators, Sensors) for the SIRI function of iPhones
#### Performance Measure
1. Speed
2. Accuracy of the result

#### Environment
1. Language(s)
2. Internet connection

#### Actuators
1. Screen Display
2. Audio Output

#### Sensor
1. Audio Input (microphone)
2. Input from keyboard


### 3. Tower of Hanoi
a) A state is any configuration of disks on the peg
- 3 tuples representing left middle right poles
- the tuples contains the disks and sizes of the disks
b) The invariant is that all disks must be placed with ascending order where a disk of smaller diameter cannot be below a disk of larger diameter
- numbers have to be in ascending order
c) The initial state has the n disks on the initial peg sorted in order by diameter, with the largest at the bottom and the smallest at the top. The goal state is the same configuration with all the disks stacked on the end peg.
d) The actions are the movement of one disk from the initial peg to a destination peg.
- 6 total actions, left right middle to the other 2 not chosen
e) The transition function T is when the resulting next state is created by removing one disk from a peg and placed on another peg.
T((1), (2,3), ()) -> T((1,2,3), (), ())


### 4. Undirected graph
a) State of the Priority Queue in tree search:
(SA, 1), (SB, 5), (SC, 15)
(SB, 5), (AG, 10), (SC, 15)
(BG, 5), (AG, 10), (SC, 15)
The search will end when the path BG is removed and the final path will be S -> B -> G

cumulative path cost, continue adding
inefficient as the frontier keeps expanding


b) State of the set in graph search:
(SA, 1), (SB, 5), (SC, 15) 
(SB, 5), (AG, 11), (SC, 15)
(BC, 10), (AG, 11), (SC, 15)

c) There is still a path in the priority queue that has not been popped and thus the path to the goal is not seen by the goal.  

d) Uniform-cost search only evaluates the cost to the start vertex when we choose a vertex to expand while djikstras algorithm determines the lowest cost from the root to every node
Actually equivalent.

### 5. Describe a state space in which iterative deepening search performs much worse than depth-first seach
When the state space is a large, shallow tree. In this case, the goal state is located close to the root of the tree, and the tree is not very deep. Hence, depth first search will be much quicker in finding the correct node while the IDS will spend a lot of time increasing the depth limit and revisiting the same states over and over again. Since IDS is a BFS pretending to be a DFS

Larger branching factor b where all nodes at depth d are solutions. IDS will go through all nodes before the solutions while DFS will get to the bottom to get to the solution.