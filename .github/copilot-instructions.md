# MCA Python Course Content - AI Agent Instructions

## Project Overview
This is a **Sphinx-based educational documentation repository** for Mohan Babu University's MCA first-year Python programming course. The project generates static HTML documentation deployed to GitHub Pages at `https://mbu-official.github.io/mca_python_course_content_2025/`.

## Architecture & Structure

### Documentation Organization
- **Content**: All course materials are in `docs/source/` as `.rst` (reStructuredText) files
- **Naming convention**: `module{N}_{topic_name}.rst` (e.g., `module1_features_and_history_of_python.rst`)
- **Navigation**: Structured by three modules (Module 1-3), each ending with `module{N}_assignment.rst`
- **Index file**: `docs/source/index.rst` contains the master TOC and course overview with all module links

### Module Structure (Pattern)
1. **Module 1** (7 periods): Python basics, I/O, operators, data types
2. **Module 2** (7 periods): Control flow, loops, comprehensions, exception handling
3. **Module 3** (10 periods): Data structures, strings, functions, recursion

Each module follows: conceptual topics → practical examples → assignment questions

## Development Workflows

### Building Documentation Locally
```powershell
# Install dependencies (uses uv for package management)
pip install -r pyproject.toml  # or use uv

# Build HTML docs
cd docs; sphinx-build -b html source build/html

# Live preview with auto-rebuild
sphinx-autobuild source build/html
```

### CI/CD Pipeline
- **Trigger**: Push/PR to `main` branch
- **Process**: `.github/workflows/deploy-docs.yml` runs Sphinx build → deploys to GitHub Pages
- **Dependencies**: Installs `sphinx`, `furo`, `myst-parser`, `sphinx-autobuild` from pip (not pyproject.toml - see workflow file)

## Content Conventions

### reStructuredText Patterns
```rst
.. _module_reference_name:

Topic Title
===========

Section Heading
---------------

Subsection
~~~~~~~~~~

.. code-block:: python

   # Python examples always use this directive
   print("Hello")

.. note::
   Used for special instructions (e.g., "Do not use loops" in assignments)
```

### Assignment Questions Format
- Start with `.. note::` for constraints (e.g., "no conditionals allowed")
- Use **bold for question titles** (e.g., `**1. Swapping Variables**`)
- Include *Hint:* in italics after each question
- Questions are numbered sequentially (1, 2, 3...)

### Code Examples
- All Python code uses `.. code-block:: python` directive
- Include inline comments for clarity
- Show both syntax and practical examples
- For assignments: emphasize constraints (no imports, no loops, etc.)

## Theme & Styling
- **Theme**: Furo (modern, clean Sphinx theme)
- **Colors**: Brand primary `#2962FF` (light), `#82B1FF` (dark)
- **Announcement**: "Welcome to the Python Course Documentation"
- **Extensions**: `autodoc`, `napoleon`, `viewcode`, `todo`, `autosummary`, `myst_parser`

## Critical Context
- **Target audience**: MCA first-year students (beginner level)
- **Pedagogy**: Theory + code snippets + assignments (no separate code files/notebooks)
- **Educational constraint**: Assignment questions often prohibit advanced features to reinforce fundamentals
- **Curator**: Zaid Kamil (referenced in copyright and README)
- **Institution**: Mohan Babu University (2025)

## When Adding/Modifying Content

1. **New topic**: Create `module{N}_{topic}.rst` in `docs/source/` and add to `index.rst` TOC
2. **Code examples**: Always use `.. code-block:: python` with explanatory comments
3. **Cross-references**: Use `:doc:` role for internal links (e.g., `:doc:`Strings <module3_strings>`)
4. **Images**: Place in `docs/source/_static/` and reference with `.. image::` directive
5. **Testing**: Build locally before pushing to catch RST syntax errors

## External Dependencies
- **Sphinx**: 8.2.3+
- **Theme**: furo 2025.7.19+
- **Python**: 3.13+ (per `.python-version` and `pyproject.toml`)
- **Package manager**: uv (see `uv.lock`)
