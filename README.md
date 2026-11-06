# Exp No: 10 – Implementation of Classical Planning Algorithm
<h3>Name: LOKESH B  </h3>
<h3>Register Number/Staff Id:   212224040172             </h3>
## Aim

To implement a **Classical Planning Algorithm** using a search strategy to find a sequence of actions that transforms an initial state into a desired goal state.

## Problem Statement

Given an initial state, a goal state, and a set of actions with their preconditions and effects, implement the `find_plan()` method to find a valid sequence of actions that transforms the initial state into the goal state.

## Algorithm / Procedure

1. Define the initial state.
2. Define the goal state.
3. Define the available actions with their preconditions and effects.
4. Start the search from the initial state.
5. Use **Breadth-First Search (BFS)** to explore possible states.
6. Check whether the current state satisfies the goal state.
7. If the goal is reached, return the sequence of actions.
8. Otherwise, check the preconditions of each action.
9. Apply the effects of valid actions to generate new states.
10. Add unexplored states to the queue.
11. Continue until the goal state is reached or no solution exists.
12. Print the generated plan.

## Program / Code

```python
from collections import deque


def find_plan(initial_state, goal_state, actions):

    def is_goal(state):
        return all(
            state.get(key) == value
            for key, value in goal_state.items()
        )

    def apply_action(state, action):
        new_state = state.copy()
        new_state.update(action['effect'])
        return new_state

    def state_key(state):
        return tuple(sorted(state.items()))

    queue = deque()
    queue.append((initial_state, []))

    visited = {state_key(initial_state)}

    while queue:

        current_state, plan = queue.popleft()

        # Check whether goal is reached
        if is_goal(current_state):
            return plan

        # Try all available actions
        for action_name, action in actions.items():

            # Check preconditions
            if all(
                current_state.get(key) == value
                for key, value in action['precondition'].items()
            ):

                # Apply action
                new_state = apply_action(
                    current_state,
                    action
                )

                key = state_key(new_state)

                if key not in visited:
                    visited.add(key)

                    new_plan = plan + [action_name]

                    queue.append(
                        (new_state, new_plan)
                    )

    return None


# Initial State
initial_state = {
    'A': 'Table',
    'B': 'Table'
}

# Goal State
goal_state = {
    'A': 'B',
    'B': 'Table'
}

# Actions
actions = {

    'move_A_to_B': {
        'precondition': {
            'A': 'Table',
            'B': 'Table'
        },
        'effect': {
            'A': 'B'
        }
    },

    'move_B_to_Table': {
        'precondition': {
            'A': 'Table',
            'B': 'B'
        },
        'effect': {
            'B': 'Table'
        }
    }
}


# Find the plan
plan = find_plan(
    initial_state,
    goal_state,
    actions
)

print(plan)
```

## Sample Input / Output

### Sample Input

```text
Initial State:
{'A': 'Table', 'B': 'Table'}

Goal State:
{'A': 'B', 'B': 'Table'}
```

### Sample Output

```text
['move_A_to_B']
```

## Output

<img width="1730" height="257" alt="image" src="https://github.com/user-attachments/assets/d59b3516-1f87-46a6-a268-af1710fb8e6e" />


## Result

Thus, the **Classical Planning Algorithm** was successfully implemented using **Breadth-First Search (BFS)**, and a valid sequence of actions was obtained to reach the goal state.
