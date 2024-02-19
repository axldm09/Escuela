
```
Below is the pseudocode of the Bidirectional Search:

BIDIRECTIONAL_SEARCH
QI.Insert(xI) and mark xI as visited
QG.Insert(xG) and mark xG as visited
while QI not empty and QG not empty do
    if QI not empty
        x ← QI.GetFirst()
    if x = XG or I E QG
        return SUCCESS
    forall u E U(x)
        x' ← f(x, u)
        if x' not visited
            Mark x' as visited
            QI.Insert(x')
        else
            Resolve duplicate x'
    if QG not empty
        x' ← QG.GetFirst()
        if x' ← x or r' E QI
            return SUCCESS
    forall u-1 E U-1(x')
        x ← f-1(x',u-1)
        if x not visited
            Mark x as visited
            QG.Insert(x)
        else
            Resolve duplicate x
return FAILURE

```

```
function BIBFS-SEARCH(problemF, problemB) returns a solution node, or failure
nodeF ← NODE(problemF.INITIAL)  // Node for a start state
nodeB ← NODE(problemB.INITIAL)  // Node for a goal state
frontierF ← a queue with nodeF as an element
frontierB ← a queue with nodeB as an element
reachedF ← a set with nodeF.STATE as an element
reachedB ← a set with nodeB.STATE as an element
solution ← failure

while not TERMINATED(solution, frontierF, frontierB) do
    solution ← PROCEED(F, problemF, frontierF, reachedF, reachedB, solution)
    if solution is not failure then
        return solution

    solution ← PROCEED(B, problemB, frontierB, reachedB, reachedF, solution)
    if solution is not failure then
        return solution

function PROCEED(dir, problem, frontier, reached, reached2, solution) returns a solution
    // Expand node on frontier; check against the other frontier in reached2.
    // The variable “dir” is the direction: either F for forward or B for backward.
    node ← DEQUEUE(frontier)
    for each child in EXPAND(problem, node) do
        s ← child.STATE
        if s not in reached or PATH-COST(child) < PATH-COST(reached[s]) then
            reached[s] ← child
            ENQUEUE(frontier, child)

        if s in reached2 then
            solution2 ← JOIN-NODES(dir, child, reached2[s])
            if PATH-COST(solution2) < PATH-COST(solution) then
                solution ← solution2

    return solution
```



```
function BIBFS-SEARCH(problemF, problemB) returns a solution node, or failure
nodeF ← NODE(problemF.INITIAL)  // Node for a start state
nodeB ← NODE(problemB.INITIAL)  // Node for a goal state
frontierF ← a queue with nodeF as an element
frontierB ← a queue with nodeB as an element
reachedF ← a set with nodeF.STATE as an element
reachedB ← a set with nodeB.STATE as an element
solution ← failure

while not TERMINATED(solution, frontierF, frontierB) do
    solution ← PROCEED(F, problemF, frontierF, reachedF, reachedB, solution)
    if solution is not failure then
        return solution

    solution ← PROCEED(B, problemB, frontierB, reachedB, reachedF, solution)
    if solution is not failure then
        return solution

function PROCEED(dir, problem, frontier, reached, reached2, solution) returns a solution
    // Expand node on frontier; check against the other frontier in reached2.
    // The variable “dir” is the direction: either F for forward or B for backward.
    node ← DEQUEUE(frontier)
    for each child in EXPAND(problem, node) do
        s ← child.STATE
        if s not in reached then
            reached[s] ← child
            ENQUEUE(frontier, child)

        if s in reached2 then
            solution2 ← JOIN-NODES(dir, child, reached2[s])
            if solution is failure or LENGTH(solution2) < LENGTH(solution) then
                solution ← solution2

    return solution

```