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

**Stack (last in, first out)** - <u>depth first search</u>, I.e., search algorithm that always expands the deepest node in the frontier

**Queue (first in, first out)** - <u>breadth first search</u>, I.e., search algorithm that always expands the shallowest node in the frontier

