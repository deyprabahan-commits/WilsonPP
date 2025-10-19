import random
from collections import defaultdict

def neighbors(cell, w, h):
x, y = cell
for dx, dy in ((1,0),(-1,0),(0,1),(0,-1)):
nx, ny = x+dx, y+dy
if 0 <= nx < w and 0 <= ny < h:
yield (nx, ny)

def advanced_choice(neighs, tree, walk_set, w, h, alpha=2, beta=1.5, gamma=0.5):
weights = []
for n in neighs:
# neighbors already in tree
in_tree_count = sum(1 for nn in neighbors(n, w, h) if nn in tree)
# neighbors in current walk (loop history)
in_walk_count = sum(1 for nn in neighbors(n, w, h) if nn in walk_set)
# distance-based bias: farther from tree is slightly favored
dist_weight = 1 + gamma * (len(neighs) - in_tree_count)
weight = (1 / (1 + in_tree_count))**alpha * (1 / (1 + in_walk_count))**beta * dist_weight
weights.append(max(0.01, weight))
return random.choices(list(neighs), weights=weights, k=1)[0]

def wilson_pp_advanced(width, height, seed=None, meta_cells=None, levels=2):
if seed is not None:
random.seed(seed)

cells = [(x,y) for y in range(height) for x in range(width)]                
unvisited = set(cells)                
maze = {c: set() for c in cells}                
                
# Multiple seeds                
num_seeds = max(1, int((width*height)**0.5 / 4))                
seeds = random.sample(cells, num_seeds)                
tree = set(seeds)                
unvisited -= tree                
                
while unvisited:                
    # pick random unvisited cell                
    ucell = random.choice(list(unvisited))                
    walk = [ucell]                
    walk_set = {ucell}                
                    
    while walk[-1] not in tree:                
        cur = walk[-1]                
        neighs = list(neighbors(cur, width, height))                
        nxt = advanced_choice(neighs, tree, walk_set, width, height)                
                        
        if nxt in walk_set:                
            idx = walk.index(nxt)                
            # dynamic loop retention                
            keep_prob = 0.3 + 0.4 * (len(neighs)/4)                
            if random.random() < keep_prob:                
                walk = walk[:idx+1] + walk[idx+1:]                
            else:                
                walk = walk[:idx+1]                
            walk_set = set(walk)                
        else:                
            walk.append(nxt)                
            walk_set.add(nxt)                
                    
    # Merge walk into tree                
    for i in range(len(walk)-1):                
        a, b = walk[i], walk[i+1]                
        maze[a].add(b)                
        maze[b].add(a)                
        tree.add(a)                
        unvisited.discard(a)                
    tree.add(walk[-1])                
    unvisited.discard(walk[-1])                
                
# Multi-level meta-cell refinement                
if meta_cells:                
    for level in range(levels):                
        size = meta_cells // (2**level)                
        for mx in range(0, width, size):                
            for my in range(0, height, size):                
                local_cells = [(x,y) for x in range(mx, min(mx+size, width))                
                                      for y in range(my, min(my+size, height))]                
                random.shuffle(local_cells)                
                for i in range(len(local_cells)-1):                
                    a, b = local_cells[i], local_cells[i+1]                
                    maze[a].add(b)                
                    maze[b].add(a)                
                
return maze

ASCII renderer unchanged

def print_maze(maze, w, h):
out = []
for y in range(h):
top = []
mid = []
for x in range(w):
cell = (x,y)
top.append("+" + ("   " if (x,y-1) in maze[cell] else "---"))
mid.append((" " if (x-1,y) in maze[cell] else "|") + "   ")
out.append("".join(top) + "+")
out.append("".join(mid) + "|")
out.append("+" + ("---+"*w))
print("\n".join(out))

if name == "main":
w, h = 20, 12
maze = wilson_pp_advanced(w, h, seed=42, meta_cells=4, levels=2)
print_maze(maze, w, h)

