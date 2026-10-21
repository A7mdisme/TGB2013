# Lab 1: Search Foundations on an Airline Network

This package arranges the supplied files into the structure expected by the lab.
The algorithm and lab source files are unchanged. The supplied requirnments.txt
has been copied as requirements.txt. Sample results from a verified run are included.

## Windows setup (Command Prompt)

Extract the archive. Open the AI folder in VS Code. Open a Command Prompt terminal
in that folder, then run:

```bat
py -3 -m venv .venv
.venv\Scripts\activate.bat
python -m pip install numpy pandas matplotlib pytest
python -m pytest all_experiments\utils -q
python all_experiments\lab01_search_foundations.py
```

Python 3.10 or newer is required by the type annotations. In VS Code, select the
.venv interpreter with Python: Select Interpreter. Jupyter is not required.
The full supplied requirements.txt also contains dependencies for other work;
the four packages above are sufficient for this lab and its tests.

## Folder layout

- all_datasets/: the two airport and route CSV files
- all_experiments/lab01_search_foundations.py: the lab to run
- all_experiments/utils/: helper code, search queries and tests
- results/lab01/: metrics.csv and route_comparison.png

Do not put all Python files into one folder: the script imports the utils package.

## Understanding the six questions

1. Load and clean the graph: airports are nodes and directed routes are edges.
   Cleaned data: 6,464 airports and 37,337 unique valid directed routes.
2. Assign each edge a great-circle distance in kilometres with the Haversine formula.
   These are geographic distances, not fares or actual flown distances.
3. Run BFS, DFS and UCS for KUL to KEF, SIN to EZE, and NRT to CPT.
4. Validate that every path uses existing routes and that its edge costs sum correctly.
5. Compare hops, distance, search effort and the effect of neighbour order on DFS.
6. Save the metrics table and the route comparison figure.

## Algorithms

- BFS (breadth-first search) uses a queue to explore shallow levels first.
  It minimizes flight legs, not distance.
- DFS (depth-first search) uses a stack and explores deeply.
  It does not guarantee fewest legs or shortest distance; neighbour order matters.
- UCS (uniform-cost search) uses a priority queue ordered by accumulated cost.
  It minimizes total distance for this graph's non-negative edge costs.

A hop means one flight leg; intermediate stops equal hops minus one for these routes.
Expanded counts states whose neighbours were generated. Max frontier measures
peak queued search entries, not memory in bytes. Runtime varies between runs and
includes result construction; small single-run differences are not decisive.
The figure uses longitude/latitude axes and is not a geographic map projection.

## Verified sample results

| Query | BFS legs / km | DFS legs / km | UCS legs / km |
| --- | --- | --- | --- |
| KUL to KEF | 2 / 12,274 | 23 / 41,768 | 4 / 11,461 |
| SIN to EZE | 2 / 21,976 | 39 / 65,214 | 3 / 17,817 |
| NRT to CPT | 2 / 19,006 | 64 / 91,541 | 3 / 14,813 |

All eight supplied tests passed. All nine computed paths passed the lab's checks.
Rerunning overwrites the sample result files. Routes describe the supplied dataset,
not current flight availability.

No separate assignment brief or marking rubric was supplied. Check your instructor's
requirements before deciding what to submit; this guide does not establish them.
