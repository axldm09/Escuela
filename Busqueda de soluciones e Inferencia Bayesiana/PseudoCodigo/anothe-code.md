```python
def bidirectional_search(problem):
    initial_state = problem.initial_state
    goal_state = problem.goal_state

    forward_frontier = [initial_state]
    backward_frontier = [goal_state]

    forward_explored = set()
    backward_explored = set()

    while forward_frontier and backward_frontier:
        forward_node = forward_frontier.pop(0)
        backward_node = backward_frontier.pop(0)

        forward_explored.add(forward_node)
        backward_explored.add(backward_node)

        if forward_node == goal_state or forward_node in backward_explored:
            return "Goal found"

        if backward_node == initial_state or backward_node in forward_explored:
            return "Goal found"

        forward_neighbors = problem.get_successors(forward_node)
        backward_neighbors = problem.get_predecessors(backward_node)

        for neighbor in forward_neighbors:
            if neighbor not in forward_explored and neighbor not in forward_frontier:
                forward_frontier.append(neighbor)

        for neighbor in backward_neighbors:
            if neighbor not in backward_explored and neighbor not in backward_frontier:
                backward_frontier.append(neighbor)

    return "Goal not found"

```