# Informed Search

## 1. Pacman 
 One heuristic for a Pac-Man game could be searching for the closest food dot on the map from the pacman. Using Manhattan distance, the pacman will try to reduce the distance to the closest pellet. This is non trivial as the closest pellet wil always change depending on the state of the board. This heuristic is admissible because the actual cost of reaching the closest pellet will always be less than or equal to the estimated cost.

Simple heuristic is a state with n as the number of pellets left on the state.


## 2. Route finding 
### a)
It is a admissible heuristic. Just like the triangle, straight line distance of one side is alwasy less than or equal than that of the longest side.

### b)
It is not an admissible heuristic. Taking the sum of 2 sides, its possible that it be longer than the hypotenuse side. (0,0) and (1,1) is root(2) but

### c)
hsld(n). 


## 3. 
### a) 
Given that h(G) = 0 and if it is consistent, then it must satisfy the triangle inequality where h(n) ≤ c(n,a,n') + h(n') and c(n,a,n') is the cost to move from n to m. If h(G) = 0, the estimated cost of reaching any goal from state n to G is just h(G), which is equal to the cost of reaching the goal. Hence cost of using h will never be greater than the cost of reaching the goal thus making h admissible.

### b)
3 nodes from 


## 4.


## 5. 
### a) 
