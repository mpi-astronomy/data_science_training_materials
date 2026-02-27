1. Minimal Viable Documentation (Scientific Context)

The least documentation your code should have is a README file. 

Your README Should Answer

What (scientific) problem does this solve?

What dataset/survey does it target?

What are the inputs?

What are the outputs?

What assumptions does it make?

How do I reproduce a figure from the paper?

## Minimal Viable Docs (README vs. Real Docs)

### Documentation Is a Scientific Issue

In astronomy, software is rarely “just code.” It often:

- Produces figures in papers
- Generates catalogs
- Encodes physical assumptions
- Implements analysis pipelines
- Trains statistical or machine learning models

Therefore, documentation is not primarily about developer convenience. It is about:

- Scientific transparency
- Reproducibility
- Reusability
- Long-term maintainability
- Correct interpretation of physical assumptions

A repository that produced published results but cannot be understood by someone outside the original author’s group represents a reproducibility risk.

Minimal viable documentation is the smallest amount of documentation that makes the software scientifically interpretable and practically usable by someone else.


### What "Minimal Viable" Means
Minimal viable documentation means only what is necessary—nothing decorative, nothing redundant, but everything essential:
- Clear statement of scientific purpose
- Explicit assumptions (units, cosmology, priors)
- Input and output formats
- Reproducibility instructions
- Citation information

The goal is not to write a textbook. The goal is to remove ambiguity.

### The Role of the README
A README is a great entry point. It should answer six questions:
1. What (scientific) problem does this solve? The physical problem; the target dataset (e.g., survey, simulation); the known limitations. Explicit assumption: cosmology, units, magnitudes, coordinae systems, etc.
2. Why does this tool exist (what gap does it fill)? What's the methodological gap? Why is not existing software sufficient?
(3. Who is it for?)
4. How do I install it? what are the depenancies?
5. What is the simplest working example? Imports the package, runs one core function, produces a small output
6. How do I cite it? - you don't have to have a paper to make the code citeable. 

### What Makes a Scientific README Different
- **Scientific Context**: Physical problem, target dataset, known limitations
- **Explicit Assumptions**: Cosmology, units, magnitude system, coordinate convention
- **Data Requirements**: File format, required columns, units, preprocessing
- **Minimal Reproducible Example**: A code snippet that imports, runs, and produces output
- **Reproducing Published Results**: Instructions for reproducing figures or tables

### Other Documentation Types
Beyond the README, other documentation includes:
- **Comments in the code**: write as you go, document assumptions, failures, to do's
- **API Reference**: Precise function documentation with units and assumptions
- **Tutorials**: Learning-oriented, step-by-step examples
- **Science Paper**: Scientific context and method justification
- **JOSS Paper**: Design Choices, comparison to the field

Examples:
Good: https://github.com/mpi-astronomy/ai-agents
Passable: https://github.com/mpi-astronomy/snowblind 
Could do better: https://github.com/lkreidberg/batman (but it has other docs)


## Smart project structure & architecture patterns
📌 Why Structure & Architecture Matter

In scientific code, structure is not a stylistic choice — it determines:

- Reproducibility
- Testability
- Extendability
- Collaboration between students/postdocs
- Ease of publication (JOSS, PyPI)

Astronomy code often starts as notebooks and scripts, and that is fine early on. But as a project grows (especially when tied to papers or pipelines), randomness in structure becomes a hidden cost.

A clean structure reduces cognitive load: you know where logic lives, where IO lives, and where workflows are orchestrated.

### A minimal project:

A minimal, well-structured scientific Python project typically looks like:

```python
project-name/
├── pyproject.toml
├── README.md
├── LICENSE
├── CHANGELOG.md
├── src/
│   └── project_name/
│       ├── __init__.py
│       ├── io.py
│       ├── physics.py
│       ├── models.py
│       ├── analysis.py
│       └── cli.py
├── tests/
│   └── test_physics.py
├── docs/
│   ├── tutorials/
│   └── reference/
└── examples/
    └── reproduce_figure2.py
```

Example in https://github.com/mpi-astronomy/mpia-python-template

### Core Principles
1. Separation of Concerns (SoC)

What it is: Divide your code by responsibility, not by data source or by notebook.
Why it matters: Mixing IO with physics logic hides assumptions and makes unit testing near impossible.


Bad: 
```python
def compute_mass_from_fits(file):
    data = fits.open(file)
    ...
    do calculation
```

Good:
```python
def load_catalog(file) -> Table: ...
def compute_stellar_mass(data: Table) -> np.ndarray: ...
```

The good version separates IO (loading) from physics (computation), making each function testable and reusable independently.

2. Modularity

Break complex tasks into small, reusable units.

Modules could be organized by:
- IO (FITS/HDF5/Catalog readers)
- Physics (equations, models)
- Models (ML/statistical models)
- Analysis (workflows)
- CLI (user interfaces)

This organization improves clarity, enables independent testing, makes reuse easier

3. Explicit Arguments (No Hidden Globals)

Scientific code often gets tempted to use global objects like: default cosmology, hidden config files, hard-coded paths

Bad:
```python
compute_mass(data)  # uses hidden global cosmology
```

Good: 
```python
compute_mass(data, cosmology=Planck18) # explicit cosmology
```

4. Thin Notebooks

Notebooks belong in `examples/` or `docs/`, not inside `src/`.

Notebooks should:
Call functions defined in `src/`
Contain minimal logic
Be reproducible end-to-end

If logic appears first in a notebook, the code architecture is not yet extractable.

Bad:
```python
notebook:
   loads data
   computes metrics
   saves figures
   prints tables
```

Good:
```
src/project_name/io.py
src/project_name/compute.py
src/project_name/plots.py
src/project_name/cli.py
tests/test_compute.py
```

Notebook becomes the orchestrator:
```python
from project_name.io import load_data
from project_name.compute import compute_mass
from project_name.plots import plot_mass

data = load_data()
mass = compute_mass(data)
plot_mass(mass)
```

## Packaging Python projects — the minimal viable way

Most astronomy repos:

```python
project/
  script1.py
  script2.py
  helper.py
  final_notebook.ipynb
```
Why is this not great?

### When Should Research Code Become a Package?

Criteria:
- Used in more than one notebook
- Used by more than one person
- Generates a figure in a paper
- Shared with collaborators
- Intended for reuse

Are you copy-pasting blocks of code across notebooks? Across folders? **STOP**

### Packaging is Reproducibility Infrastructure

Packaging is not about publishing your code. Or even about anyone being able to see it. It is about:

Stable imports
Reproducible environments
CI compatibility
Eventually, maybe, publishing (JOSS eligibility)
Long-term maintainability

This mindset shift is the key.

https://github.com/mpi-astronomy/mpia-python-template

## Ruff, linters & pre-commit (fast wins, huge payoff)

### Why This Matters in Research Software

**In astronomy, code is often:**
Written quickly to test an idea
Modified repeatedly during paper preparation
Touched by multiple students/postdocs
Reused months or years later

**This leads to:**
Inconsistent style
Unused imports
Shadowed variables
Silent bugs
Debug prints left in analysis
Dead code after refactors

Linters and pre-commit hooks address these issues automatically. They reduce cognitive load and catch mistakes before they propagate into figures or results. 

**A linter** is a static tool A linter is a static analysis tool that: 
Inspects code without running it
Detects common errors
Enforces style and structure rules
Flags potential bugs

Examples of issues linters detect: unused variables, undefined names, duplicate imports, mutable default arguments, accidental shadowing, syntax issues, formatting inconsistencies

Linters do not change your scientific logic.

Doesn't VS Code already do this? Yes, to some extent. On individual files.

Linters enforce this on a project level, editor independent, for all users, doesn't depend on how you feel today.

Examples:

```python
import numpy as np
import pandas as pd # but never used
```

```python
mass = compute_mass(data)
for mass in mass_array: # variable overshadowing
    ...
```

```python
def run_pipeline(config={}): # mutable default argument, dict or a list or a set
    ...
``` 

```python
print("CHECK THIS") # forgotten debug statement
```

**And pre-commit hooks** automate it. 

 
## Avoiding “future you hates past you”

Top 10 Rules to Avoid “Future You Hates Past You”

1. Rule: Structure your project with clear separation of roles.
Why: A disciplined layout makes navigation, reuse, and automation predictable. Avoid mixing scripts and logic files; prefer a src/ folder with modules for IO, core logic, models, CLI, and tests as in modern Python templates.

2. Rule: Always include a proper packaging setup (pyproject.toml).
Why: Packaging makes installation reproducible and enables CI/linting and later publication; avoid leaving the project as just a folder of scripts without defined metadata.

3. Rule: Write minimal but complete documentation.
Why: Future readers (and reviewers) need quick orientation; avoid bare or missing README sections like installation, example usage, assumptions, and citation; prefer explicit narrative that shows what the project does and how to use it.

4. Rule: Invest in reproducible tests.
Why: Tests codify the intended scientific behavior and catch regressions; avoid “tested once manually”; prefer automated tests for edge cases, invariants, and critical computations.

5. Rule: Use meaningful names everywhere.
Why: Names are the first form of documentation; avoid opaque/temporary names like tmp, data2, or calc_final; prefer descriptive names like read_survey_catalog, fit_stellar_population, or redshift_grid.

6. Rule: Make assumptions (units, conventions, cosmology) and dependencies explicit.
Why: Hidden assumptions are silent bugs; avoid undocumented global defaults and implicit constants; prefer explicit parameters and clearly versioned dependencies in your packaging metadata.

7. Rule: Automate hygiene with formatting, linting, and pre-commit.
Why: Prevents trivial style and logic issues early; avoid only editing code manually; prefer tools like Ruff + pre-commit so that consistency is enforced in every commit.

8. Rule: Document how your code relates to published results.
Why: Scientific relevance is the core of research software; avoid “figure scripts buried in notebooks”; prefer reproducible example scripts in examples/ and narrative documentation explaining how to reproduce published figures.

9. Rule: Include citation metadata (e.g., CITATION.cff).
Why: Software is part of the science record; avoid no guidance for citation; prefer machine-readable citation files so others can easily cite the code.

10. Rule: Clean up, archive, and automate release workflows.
Why: Research tools evolve; avoid ad-hoc final touches; prefer versioned releases (tags), a CHANGELOG, CI that runs tests and publishes docs, and a clear process for tagging scientific code states.

## New JOSS submission guidelines

https://joss.readthedocs.io/en/latest/submitting.html

What is new:

Scope and significance
https://joss.readthedocs.io/en/latest/submitting.html#scope-and-significance

AI Usage Policy:
https://joss.readthedocs.io/en/latest/submitting.html#ai-usage-policy