# Wilson++ Maze Generator 

**Wilson++** is a next-level maze generation algorithm—an enhanced version of the classic **Wilson's Algorithm**.  
It introduces weighted random walks, multiple seed nodes, probabilistic loop retention, and hierarchical meta-cell refinement for more organic and complex mazes.  

---

## Features 
- Weighted neighbor selection with tunable parameters (`alpha`, `beta`, `gamma`)  
- Multiple starting seeds for faster maze coverage  
- Probabilistic loop retention for more natural maze paths  
- Multi-level meta-cell refinement to balance local and global connectivity  
- Pure Python implementation (no external dependencies)  
- ASCII maze rendering for quick visualization  

---

## Installation 

Clone the repo:

```bash
git clone https://github.com/YOURUSERNAME/WilsonPP.git
cd WilsonPP

No external dependencies—Python 3.x is enough.


---

Usage 

from wilson_pp import wilson_pp_advanced, print_maze

width, height = 20, 12
maze = wilson_pp_advanced(width, height, seed=42, meta_cells=4, levels=2)
print_maze(maze, width, height)

Parameters Explained:

width, height: dimensions of the maze

seed: random seed for reproducibility

meta_cells: number of meta-cells for hierarchical refinement

levels: number of hierarchical refinement levels


Tweak alpha, beta, gamma inside advanced_choice() for different maze generation behavior.


---

License 

This project is licensed under the GNU General Public License v3.0 (GPLv3).
See LICENSE for details.

You are free to use, modify, and distribute this project as long as derivative works are also GPLv3.


---

Contribution 

Feel free to contribute! Fork the repo, tweak the parameters, improve visualization, or implement new features. All contributions are welcome under GPLv3.


---

Author 

Prabahan
Epic maze innovator. 
