# DFS_Graph

## DFS
### Code : [main.py](file_path)
```
romania_graph = {
    "Arad": {"Zerind": 75, "Timisoara": 118, "Sibiu": 140},
    "Zerind": {"Oradea": 71, "Arad": 75},
    "Oradea": {"Zerind": 71, "Sibiu": 151},
    "Sibiu": {"Arad": 140, "Oradea": 151, "Fagaras": 99, "Rimnicu Vilcea": 80},
    "Timisoara": {"Arad": 118, "Lugoj": 111},
    "Lugoj": {"Timisoara": 111, "Mehadia": 70},
    "Mehadia": {"Lugoj": 70, "Drobeta": 75},
    "Drobeta": {"Mehadia": 75, "Craiova": 120},
    "Craiova": {"Drobeta": 120, "Rimnicu Vilcea": 146, "Pitesti": 138},
    "Rimnicu Vilcea": {"Sibiu": 80, "Craiova": 146, "Pitesti": 97},
    "Fagaras": {"Sibiu": 99, "Bucharest": 211},
    "Pitesti": {"Rimnicu Vilcea": 97, "Craiova": 138, "Bucharest": 101},
    "Bucharest": {"Fagaras": 211, "Pitesti": 101, "Giurgiu": 90},
    "Giurgiu": {"Bucharest": 90},
}

visited = set()

def dfs(root, goal):
    stack = [root]
    
    while stack:
        node = stack.pop()
        
        if node == goal:
            print(node, end="->")
            return True
            
        if node not in visited:
            visited.add(node)
            print(node, end="->")
            
            for neighbour in (romania_graph[node]):
                stack.append(neighbour)
                
    return False

source = "Arad"
destination = "Bucharest"
print(dfs(source, destination))
```
### Output :
````
Arad->Sibiu->Rimnicu Vilcea->Pitesti->Bucharest->True
````
## Limited_DFS
### Code :

```
romania_graph = {
    "Arad": {"Zerind": 75, "Timisoara": 118, "Sibiu": 140},
    "Zerind": {"Oradea": 71, "Arad": 75},
    "Oradea": {"Zerind": 71, "Sibiu": 151},
    "Sibiu": {"Arad": 140, "Oradea": 151, "Fagaras": 99, "Rimnicu Vilcea": 80},
    "Timisoara": {"Arad": 118, "Lugoj": 111},
    "Lugoj": {"Timisoara": 111, "Mehadia": 70},
    "Mehadia": {"Lugoj": 70, "Drobeta": 75},
    "Drobeta": {"Mehadia": 75, "Craiova": 120},
    "Craiova": {"Drobeta": 120, "Rimnicu Vilcea": 146, "Pitesti": 138},
    "Rimnicu Vilcea": {"Sibiu": 80, "Craiova": 146, "Pitesti": 97},
    "Fagaras": {"Sibiu": 99, "Bucharest": 211},
    "Pitesti": {"Rimnicu Vilcea": 97, "Craiova": 138, "Bucharest": 101},
    "Bucharest": {"Fagaras": 211, "Pitesti": 101, "Giurgiu": 90},
    "Giurgiu": {"Bucharest": 90},
}

def limited_dfs(root, goal, depth_limit):
    visited = set()
    stack = [(root, 0)]

    while stack:
        node, depth = stack.pop()

        if depth > depth_limit:
            continue

        if node == goal:
            print(node, end="->")
            return True

        if node not in visited:
            visited.add(node)
            print(node, end="->")

            for neighbor in romania_graph[node]:
                stack.append((neighbor, depth + 1))

    return False

source = "Arad"
destination = "Bucharest"
depth_limit = 3  # Define your depth limit here
print(limited_dfs(source, destination, depth_limit))
```
### Output :
````
Arad->Sibiu->Rimnicu Vilcea->Pitesti->Craiova->Fagaras->Bucharest->True
````
## Iterative_Deepening_DFS
### Code :
```
romania_graph = {
    "Arad": {"Zerind": 75, "Timisoara": 118, "Sibiu": 140},
    "Zerind": {"Oradea": 71, "Arad": 75},
    "Oradea": {"Zerind": 71, "Sibiu": 151},
    "Sibiu": {"Arad": 140, "Oradea": 151, "Fagaras": 99, "Rimnicu Vilcea": 80},
    "Timisoara": {"Arad": 118, "Lugoj": 111},
    "Lugoj": {"Timisoara": 111, "Mehadia": 70},
    "Mehadia": {"Lugoj": 70, "Drobeta": 75},
    "Drobeta": {"Mehadia": 75, "Craiova": 120},
    "Craiova": {"Drobeta": 120, "Rimnicu Vilcea": 146, "Pitesti": 138},
    "Rimnicu Vilcea": {"Sibiu": 80, "Craiova": 146, "Pitesti": 97},
    "Fagaras": {"Sibiu": 99, "Bucharest": 211},
    "Pitesti": {"Rimnicu Vilcea": 97, "Craiova": 138, "Bucharest": 101},
    "Bucharest": {"Fagaras": 211, "Pitesti": 101, "Giurgiu": 90},
    "Giurgiu": {"Bucharest": 90},
}

def dls(root, goal, depth_limit):
    stack = [(root, 0)]
    while stack:
        node, depth = stack.pop()
        if node == goal:
            print(node, end=" ")
            return True
        if depth < depth_limit:
            print(node, end=" ")
            for neighbor in romania_graph[node]:
                stack.append((neighbor, depth + 1))
    return False

def iddfs(root, goal):
    depth_limit = 0
    while True:
        print("\nDepth Limit:", depth_limit)
        if dls(root, goal, depth_limit):
            return True
        depth_limit += 1
    return False

def get_input():
    root = input("Enter the root node: ")
    goal = input("Enter the goal node: ")
    return root, goal

print("Iterative Deepening Depth-First Search (IDDFS)")
root, goal = get_input()
print("IDDFS:")
iddfs(root, goal)

```
### Output :
````
Welcome to Iterative Deepening Depth-First Search (IDDFS)
Enter the root node: Arad
Enter the goal node: Bucharest
IDDFS:

Depth Limit: 0

Depth Limit: 1
Arad 
Depth Limit: 2
Arad Sibiu Timisoara Zerind 
Depth Limit: 3
Arad Sibiu Rimnicu Vilcea Fagaras Bucharest
````
