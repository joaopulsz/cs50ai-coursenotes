# Search Problems

Consist of:

**Initial state** - a place where it begins

**Actions** - some action that can be taken or multiple actions that can be taken in any given state

**Transition model** - a way of defining what state we end up with if we take a given action at a given state

**Goal test** - to know whether or not a goal’s been reached

**Path cost function** - to know how expensive, in terms any given resource resource, taking a sequence of actions is

All these serve the purpose of finding the **most optimal solution(s)** for a given problem


### Node

Is a data structure (used to solve search problems) that keeps track of:

**A state** - the state we’re currently on

**A parent** - node that generated this node

**An action** - applied to the parent to get the current node

**A path cost** - from the initial state to the current node


### Approach

Start with a **frontier** (representation of all the the possibilities that can be explored but have no yet been explored or visited) that contains the initial state

Also start with an empty explored set

Then, repeat the following loop until the most optimal solution has been reached:
- if the frontier is empty, then no solution
	
- remove a node from the frontier

- if node contains goal state, return the solution

- add the node to the explored set

- expand node (consider all possible actions that can be taken from the state this node is representing), add resulting nodes to the frontier if they aren't already there or in the explored set


### Frontiers

Can be different data structures depending on the problem at hand:

**Stack (last in, first out)** - <u>depth-first search</u>, i.e., search algorithm that always expands the deepest node in the frontier

**Queue (first in, first out)** - <u>breadth-first search</u>, i.e., search algorithm that always expands the shallowest node in the frontier


## Informed Search

Search strategies that use knowledge specific to the problem to find solutions more efficiently

### Greedy best-first search

A search algorithm that, instead of expanding the deepest node (like DFS) or the shallowest node (like BFS), always expands the node that it thinks is closest to the goal, as estimated by a heuristic function *(h)n*, which estimates how close to the goal the next node is

### A* search

A search algorithm that expands the node with the lowest value of *g(n) + h(n)*, where g(n) is the cost to reach the current node

Optimal search if it satisfies 2 conditions:
- the heuristic h(n) must be admissable, i.e., it never underestimates the true cost (it always gets it right or underestimates) and
- it must also be consistent, i.e., the heuristic value from the current state to the goal should not be more that the heuristic value of my successor plus however much it would cost me to make that step (from current to successor)


## Adversarial Search

### Minimax algorithm

Represents winning conditions as (1) for one side, (-1) for the other, and (0) for a tie. Actions taken by this algorithm are driven by these conditions, with the maximizer side trying to get the highest score and the minimizer side trying to get the lowest score

**Tic-tac-toe AI:** 
- S*0*: initial state
- player(*s*): returns which player to move in state *s*
- action(*s*): returns legal moves in state *s*
- result(*s,a*): returns state after action *a* taken in state *s*
- terminal(*s*): checks if state *s* is a terminal state
- utility(*s*): final numerical value for terminal state *s*

**Minimax in pseudocode:**
given a state *s*: 
- The maximizing player picks action *a* in Actions(*s*) that produces the highest value of Min-Value(Result(*s, a*))
- The minimizing player picks action *a* in Actions(*s*) that produces the lowest value of Max-Value(Result(*s, a*))
function Max-value(*s*):
- if terminal(*s*): return utility(*s*)
- v = -∞
- for *a* in Actions(*s*): v = Max-value(v, Min-value(Result(*s, a*)))
- return v 
function Min-value(*s*):
- if terminal(*s*): return utility(*s*)
- v = ∞
- for *a* in Actions(*s*): v = Min-value(v - Max-value(Result(*s, a*)))
- return v 

**Optimizing the minimax algotithm:**
- alpha-beta pruning: skips some of the recursive computations that are decidedly unfavorable
- depth-limited minimax: considers only a pre-defined number of moves before it stops, without ever getting to a terminal state. It relies on an *evaluation function* that estimates the expected utility of the game from a given state, or, in other words, assigns values to states