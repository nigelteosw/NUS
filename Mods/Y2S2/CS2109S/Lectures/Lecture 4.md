# Intro to Machine Learning & Decision Trees
## Remarks on Problem Set
- When implementing DFS, do not use **Recursion**
- For memoisation make sure to create a hashatable that needs **O(1) lookup**


## Search Recap
- [[Breadth-First Search]]
- [[Depth-First Search]]
- Iterative Deepening Search (DLS implemented by DFS)
- Greedy Best-First Search
- A* Search

### Need to Understand
- Space/time tradeoffs
- Completeness/optimality conditions
- Understanding **PRUNING**: IDA*, SMA*


## Adversarial Search Recap
- Rational Opponent -> Minimax
- Solving a Game Tree
- Evaluation Function
- alpha-beta pruning
	- If at MIN node, we can stop if we find a noide that is smaller than or equal to a
	- https://pascscha.ch/info2/abTreePractice/
	- Mini Project is to implement alpha-beta minmax


## Machine Learning
- Data collection is costly, but the more data we have about the problem the easier it is to solve it
- Data is also not a simple curve, there can be inconsistent data, missing data
- Visualizing data is often helpful 
- More dimensions require exponentially more data
- P: Performance
- T: Task
- E: Experience

### Pipeline
1. Data collection 
2. Data extraction (Feature engineering) 
3. Data understanding (with Visualization) 
4. Data pre-processing 
5. Model choice / design 
6. Model training 
7. Model validation (Evaluation) 
8. Model understanding (Visualization / Explainability) 
9. Model deployment

### Types of Feedback
1. Supervised
	1. Correct answer given for each example
2. Unsupervised
	1. No answers given
	2. Find the pattern
3. Weakly supervised
	1. Correct answer given but not precise
4. Reinforcement 
	1. Occasional rewards given
	2. Robot navigating a maze


#### Supervised Learning
1. Regression
	- Predict results within a continuous output
2. Classification
	- Predict results in a discret output, map input variables into discrete categories

#### Decision Trees
- One possible representation for hypotheses
- Boolean functions, truth table row -> path to leaf
- Trivially, there is a consistent decision tree for any training set
	- Prefer to find more compact decision trees
	