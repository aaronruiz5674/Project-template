# Virtual Environments with uv

## 1 What is uv?

`uv` is a **modern Python virtual environment and dependency manager**, similar to `pip` and `conda`, but faster and easier to use.  

- It allows you to create **isolated environments** for your Python projects.  
- Manages dependencies and versions reproducibly using a **lockfile (`uv.lock`)**.  
- Lets you create your own Python packages and keep them organized.

---

## 2 Why use virtual environments?

- Avoid conflicts between dependencies from different projects.  
- Keep your project **portable** and reproducible.  
- Makes collaboration easier, as everyone uses the same package versions.

---

## 3 Initial Project Structure with uv

When you create a project with uv, it automatically generates a **clean and organized structure**. The exact structure depends on whether you initialize a library, an application, or a plugin. Below is the typical structure for a library project:


project_name/
├── README.md
├── pyproject.toml
├── uv.lock
├── src/
│ └── project_name/
│ └── init.py
├── tests/
└── docs/ (optional, add manually)



---

### Explanation of each part

- **README.md**  
  - Contains a short description of the project, instructions to run or install it, and links to documentation.  

- **pyproject.toml**  
  - The main **configuration file** for uv.  
  - Defines your project metadata (name, version, author) and dependencies.  
  - uv uses this to track installed packages and project settings.

- **uv.lock**  
  - The **lockfile** that stores the exact versions of all installed dependencies.  
  - Ensures everyone on the team uses the same versions for reproducibility.

- **src/**  
  - Contains the **source code** of your project.  
  - Inside, uv creates a folder with the **same name as your project**, which is a Python package (`__init__.py` included).  
  - Example usage:
    ```
    project_name/
    └── __init__.py
    └── module.py
    ```
    This allows you to import your modules cleanly:
    ```python
    from project_name.module import function
    ```

- **tests/**  
  - Contains **unit tests** for your project.  
  - Use this folder to ensure all your functions, data loaders, or models work correctly.  
  - Naming convention: `test_<module>.py`.

- **docs/** (optional)  
  - While uv doesn’t create this by default, it’s recommended to maintain a `docs/` folder for Markdown files with project documentation, instructions, and notes.

---

### Optional folders you can add

- **data/**  
  - For datasets, split into `raw/` (original data) and `processed/` (cleaned data).  
  - Usually added manually and ignored in Git if the datasets are large.

- **scripts/**  
  - For scripts like training, evaluation, or utility scripts that are not part of the package itself.

---


## 4 Creating a project with uv

```bash
# Create a library-style project
uv init --lib project_name

#Initialize an application-style project with a main entry point 
uv init --app <name>

#Initialize a plugin-style project that can be extended or used by other projects
uv init --plugin <name>

#Install a package as a dependency for your project. Updates pyproject.toml and uv.lock. Example: uv add numpy
uv add <package>

#Install a development-only dependency (e.g., pytest).
uv add -D <package>

#Remove a dependency from your project. Updates lockfile automatically.
uv remove <package>