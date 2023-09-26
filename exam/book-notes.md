# Notes

## 1.3 -

agent
environment
world

autonomous  agent
semi-an ag
software ag

belief state

puposive ag
nature

1.5-
Agent design space
10 dimensions:

1. Modularity

- flat – there is no organizational structure
• modular – the system is decomposed into interacting modules that can be understood on their own
• hierarchical – the system is modular, and the modules themselves are decomposed into simpler modules, each of which are hierarchical systems or simple components.

2. Planning Horizon
The planning horizon dimension is how far ahead in time the agent plans.

In the planning horizon dimension, an agent is one of the following:

• A non-planning agent is an agent that does not consider the future when it decides what to do or when time is not involved.
• A finite horizon planner is an agent that looks for a fixed finite number of stages. For example, a doctor may have to treat a patient but may have time for a test and so there may be two stages to plan for: a testing stage and a treatment stage. In the simplest case, a greedy or myopic agent only looks one time step ahead.
• An indefinite horizon planner is an agent that looks ahead some finite, but not predetermined, number of stages. For example, an agent that must get to some location may not know a priori how many steps it will take to get there, but, when planning, it does not consider what it will do after it gets to the location.
• An infinite horizon planner is an agent that plans on going on forever. This is often called a process. For example, the stabilization module of a legged robot should go on forever; it cannot stop when it has achieved stability, because the robot has to keep from falling over.

property - A relation on a single individiual (a thing, an object, entity)

x.? Computational limits Dimension

- perfect rationality: when an agent reasons about the best action without taking into account its limited computational resources
- bounded rationality: where an agent decides on the best action that it can find given its computational limitations

..
Ezt az összegzést befejezni később a tankönyv 1.5 alapján, és exercises-01-agents.pdf legalján lévő táblázat alapján.

----------- CHAPTER 3
3.1 Problem Solving as Search
Finding the best route from a current location to a destination is a search problem.
The state includes:
-mode of transportation

- the location of the traveler
- the direction of travel
The best route could mean many thing

! The Notion of search - is computation solely inside the agent

----
Heuristic knowledge: - an estimate of cost from a node to a goal.

3.2 State spaces

A state-space search problem consists of:

A state-space search problem consists of:

- a set of states
- a distinguished state called the **start state**
- for each state, a set of actions available to the agent in that state
- an **action function** that, given a state and an action, returns a new state
- a goal specified as a Boolean function, ***goal(s4)***, that is true when state s satisfies a goal, in which case ***s*** is a goal state
- a criterion that specifies the quality of an acceptable solution; for example, any sequence of actions that gets the agent to the goal state may be acceptable, or there may be costs associated with actions and the agent may be required to find a sequence that has minimal total cost.

A solution that is best according to some criterion is called an optimal solution. An agent may be satisfied with any solution that is within, say, 10% of optimal.

## 3.3 Graph searching

A directed graph consists of a set of nodes and a set of directed arcs between nodes. The idea is to find a path along these arcs from the start node to a goal node.

### 3.3.1 Formalizing Graph searching

A **directed graph** consists of

- a set ***N*** of nodes
- a set ***A*** of arcs, where an arc is an ordered pair of nodes

```text
The arc <n1,n2> is an outgoing arc from n1 and an incoming arc to n2.
```

Note for me: What notions to remember:

1. What a **directed graph** consists of
1. What are **nodes, arcs**
1. **Outgoing arc, incoming arc**
1. When is a node a **neighbor** of another node? (Check figure 3.3).A Node has a neighbor, if an arc leads to another node.(??) (if im counting the forward branching factor,how is that different from the number of neighbors a node has?)
1. What is a **path**
1. What is a **goal**?
1. What is a **start node**?
1. What is a **solution?**
1. The **cost of an arc** cost(<n1,n2>)
1. The cost of a path (sum of the cost of arcs in the path)
1. **Optimal solutions**
1. State-pace graph

1. Cycle (in a node) - a non-empty path where the end node is the same as the start node
1. DAG , a directed acyclic graph (or more correcetly, acyclic directed graph, ADG) - a graph without any cycles
1. Tree , root, leaf, parent and child
1. Forward branching factor, Backward branching factor

**Non-deterministic algorithms** - means that there are choices in the program that are left unspecified.
Two forms:

- don't care non-deterministic (select)
- don't know non-deterministic (choose)

## 3.5 Uninformed Search Strategies

***Super good explanations in the [book!](http://artint.info/3e/html/ArtInt3e.Ch3.S5.html)***

### 1. Breadth-First Search

![Breadth-First Search](image-1.png)
The frontier is implemented as ***FIFO queuq*** (as in first-in, first-out). Consider a tree-shaped graph. Suppose the start node is at the top, and the children are added in a left-to-right order.
In breadth-first search, the order in which the paths are expanded does not depend on the location of the goal. (also costs are ignored here, so it is searching the space without weights.)
In breadth-first search, each path on the frontier has either the same number of arcs as, or one more arc than, the next path on the frontier that is expanded (Check Example 3.9 for precise explanation.)
This method is guaranteed to find a solution if one exists and will find a solution with the fewest arcs.

***Breadth-first search is useful when:***

- the problem is small enough so that space is not a problem, such as when the graph is already stored, and
- a solution containing the fewest arcs is required.

### 2. Depth-First Search

The frontier is implemented as ***LIFO stack*** of paths (as in last-in,first-out).
![Depth-first Search](image.png)

Depth-first search is appropriate when

- space is restricted
- many solutions exist, perhaps with long paths, particularly for the case where nearly all paths lead to a solution, or
- the order in which the neighbors of a node are added to the stack can be tuned so that solutions are found on the first try.
It is a poor method when

- it is possible to get caught in infinite paths, which occurs when the graph is infinite or when there are cycles in the graph
- solutions exist at shallow depth, because in this case the search may explore many long paths before finding the short solutions, or
- there are multiple paths to a node, for example, on an 'n x n' grid, where all arcs go right or down, there are exponentially many paths from the top-left node, but only n^2 nodes

Depth-first search is the basis for a number of other algorithms, including iterative deepening, described next.

### 3. Iterative Deepening

Iterative deepening repeatedly calls a depth-bounded searcher, a depth-first searcher that takes in an integer depth bound and never explores paths with more arcs than this depth bound

Eventually, it will find a solution if one exists, and, as it is enumerating paths in order of the number of arcs, a path with the fewest arcs will always be found first.

To ensure it halts for finite graphs, iterative deepening search needs to distinguish between

- failure because the depth bound was reached
- failure due to exhausting the search space.

...

### 4. Lowest-Cost-First Search

For many domains, arcs have non-unit costs, and the aim is to find an optimal solution, a solution such that no other solution has a lower cost.

The search algorithms considered thus far are not guaranteed to find the minimum-cost paths; they have not used the arc cost information at all. Breadth-first search finds a solution with the fewest arcs first, but the distribution of arc costs may be such that a path with the fewest arcs is not one of minimal cost.

The simplest search method that is guaranteed to find a minimum-cost path is lowest-cost-first search (also called least-cost search or uniform-cost search), which is similar to breadth-first search, but instead of expanding a path with the fewest number of arcs, it selects a path with the lowest cost. This is implemented by treating the frontier as a priority queue ordered by the cost function.

![Figure 3.1](image-2.png)

![Figure 3.1 Lowest-cost-first search](image-3.png)

## 3.6 Informed (Heuristic) Search strategies

![Alt text](image-4.png)

### 1. A* search

### 2. Branch and Bound

befejezni

## 25/9  

### Search

### Consistency

Enforcing Arc Consistency for ***One*** Pair of Variables
...may examples. how to remove elments?
Start from the first node for example, and go through all (but gotta recheck again)
in an examaple such a:
A with Domain {1,2,3,4}
A < B constraint
B with Domain {1,2,3,4}
B < C constraint
C with Domain {1,2,3,4}

You would first remove .. from A

### Variable elimination

at example network (example : eliminating C)
represent constraints as tables !!
then ...
