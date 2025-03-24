def is_valid_move(x, y, grid, visited):
    """Check if the move is within bounds, not a wall, and not visited."""
    rows, cols = len(grid), len(grid[0])
    return 0 <= x < rows and 0 <= y < cols and grid[x][y] == 0 and (x, y) not in visited

def depth_limited_search(x, y, target_x, target_y, grid, depth, visited):
    """Performs a depth-limited DFS."""
    if (x, y) == (target_x, target_y):
        return True
    if depth == 0:
        return False
    
    visited.add((x, y))  # Mark the current cell as visited
    
    # Possible moves: up, down, left, right
    moves = [(-1, 0), (1, 0), (0, -1), (0, 1)]
    
    for dx, dy in moves:
        new_x, new_y = x + dx, y + dy
        if is_valid_move(new_x, new_y, grid, visited):
            if depth_limited_search(new_x, new_y, target_x, target_y, grid, depth - 1, visited):
                return True

    visited.remove((x, y))  # Unmark for other searches
    return False

def iddfs(grid, start_x, start_y, target_x, target_y, max_depth=6):
    """Iteratively increases depth limit and performs DFS up to max_depth."""
    for depth in range(max_depth + 1):  # Iterative deepening
        visited = set()
        if depth_limited_search(start_x, start_y, target_x, target_y, grid, depth, visited):
            return f"Path found at depth {depth} using IDDFS"
    
    return f"Path not found at max depth {max_depth} using IDDFS"

# Input processing for Case #2
grid = [
    [0, 1, 0],
    [0, 1, 0],
    [0, 1, 0]
]

start_x, start_y = 0, 0
target_x, target_y = 2, 2

# Running the algorithm
result = iddfs(grid, start_x, start_y, target_x, target_y)
print(result)





def is_valid_move(x, y, grid, visited):
    """Check if the move is within bounds, not a wall, and not visited."""
    rows, cols = len(grid), len(grid[0])
    return 0 <= x < rows and 0 <= y < cols and grid[x][y] == 0 and (x, y) not in visited

def depth_limited_search(x, y, target_x, target_y, grid, depth, visited):
    """Performs a depth-limited DFS."""
    if (x, y) == (target_x, target_y):
        return True
    if depth == 0:
        return False
    
    visited.add((x, y))  # Mark the current cell as visited
    
    # Possible moves: up, down, left, right
    moves = [(-1, 0), (1, 0), (0, -1), (0, 1)]
    
    for dx, dy in moves:
        new_x, new_y = x + dx, y + dy
        if is_valid_move(new_x, new_y, grid, visited):
            if depth_limited_search(new_x, new_y, target_x, target_y, grid, depth - 1, visited):
                return True

    visited.remove((x, y))  # Unmark for other searches
    return False

def iddfs(grid, start_x, start_y, target_x, target_y):
    """Iteratively increases depth limit and performs DFS."""
    depth = 0
    while True:
        visited = set()
        if depth_limited_search(start_x, start_y, target_x, target_y, grid, depth, visited):
            return "Path exists"
        depth += 1
        if depth > len(grid) * len(grid[0]):  # Upper bound to avoid infinite loops
            return "No path exists"

# Input processing
grid = [
    [0, 0, 1, 0],
    [1, 0, 1, 0],
    [0, 0, 0, 0],
    [1, 1, 0, 1]
]

start_x, start_y = 0, 0
target_x, target_y = 2, 3

# Running the algorithm
result = iddfs(grid, start_x, start_y, target_x, target_y)
print(result)






