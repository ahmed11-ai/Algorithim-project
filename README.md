import heapq
import math

# Coordinates of locations
locations = {
    "home": (0, 0),
    "metro_station": (2, 1),
    "main_street": (1, 3),
    "college": (4, 3)
}

# Graph: each node and its neighbors with distances
graph = {
    "home": [("metro_station", 2), ("main_street", 5), ("college", 3)],
    "metro_station": [("home", 2), ("college", 4)],
    "main_street": [("home", 5), ("college", 1)],
    "college": []
}

# Heuristic function: Euclidean distance
def heuristic(node, goal):
    x1, y1 = locations[node]
    x2, y2 = locations[goal]
    return math.sqrt((x2 - x1)**2 + (y2 - y1)**2)

# A* Algorithm
def a_star(start, goal):
    pq = []  # priority queue for (f, g, node, path)
    g_start = 0
    h_start = heuristic(start, goal)
    f_start = g_start + h_start

    heapq.heappush(pq, (f_start, g_start, start, [start]))

    visited = set()

    while pq:
        f, g, current, path = heapq.heappop(pq)

        if current == goal:
            return g, path

        if current in visited:
            continue
        visited.add(current)

        for neighbor, cost in graph.get(current, []):
            if neighbor in visited:
                continue
            new_g = g + cost
            new_h = heuristic(neighbor, goal)
            new_f = new_g + new_h
            new_path = path + [neighbor]
            heapq.heappush(pq, (new_f, new_g, neighbor, new_path))

    return float("inf"), []

# Run the program
if __name__ == "__main__":
    start = "home"
    goal = "college"
    distance, path = a_star(start, goal)

    if distance == float("inf"):
        print("No path found from home to college.")
    else:
        print("Shortest distance from home to college:", distance, "km")
        print("Path:", " -> ".join(path))








/////THE PROGRAM RUN


[Running] python -u "c:\Users\Ahmed\OneDrive\Desktop\algo project\pro.py"
Shortest distance from home to college: 3 km
Path: home -> college

[Done] exited with code=0 in 0.656 seconds
