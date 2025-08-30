# Installation and Environment Setup

## 🎯 Objective
Set up a complete Python development environment optimized for data structures and algorithms learning.

## 📋 System Requirements

### Minimum Requirements
- **Operating System**: Windows 10/11, macOS 10.14+, or Linux Ubuntu 18.04+
- **RAM**: 4GB (8GB recommended)
- **Storage**: 2GB free space
- **Internet Connection**: For package downloads and updates

### Recommended Specifications
- **RAM**: 8GB or more
- **Storage**: 5GB free space (for additional packages and projects)
- **Multiple monitors**: For code and documentation side-by-side

## 🔧 Python Installation

### Method 1: Official Python Installer (Recommended)

#### Windows Installation
1. **Download Python**
   - Visit [python.org](https://python.org)
   - Download Python 3.8+ (latest stable version recommended)
   - Choose "Windows installer (64-bit)" for most systems

2. **Installation Process**
   ```
   ✅ Check "Add Python to PATH"
   ✅ Check "Install pip"
   ✅ Choose "Customize installation"
   ✅ Select "Add Python to environment variables"
   ✅ Select "Install for all users"
   ```

3. **Verify Installation**
   ```cmd
   python --version
   pip --version
   ```

#### macOS Installation
1. **Using Official Installer**
   - Download from python.org
   - Run the .pkg installer
   - Follow installation wizard

2. **Using Homebrew (Alternative)**
   ```bash
   # Install Homebrew first if not installed
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   
   # Install Python
   brew install python
   ```

3. **Verify Installation**
   ```bash
   python3 --version
   pip3 --version
   ```

#### Linux (Ubuntu/Debian) Installation
```bash
# Update package list
sudo apt update

# Install Python 3 and pip
sudo apt install python3 python3-pip python3-venv

# Verify installation
python3 --version
pip3 --version
```

### Method 2: Anaconda Distribution
Anaconda provides Python with scientific packages pre-installed.

1. **Download Anaconda**
   - Visit [anaconda.com](https://www.anaconda.com)
   - Download Anaconda Individual Edition
   - Choose your operating system

2. **Installation**
   - Run the installer
   - Follow the installation wizard
   - Choose to add Anaconda to PATH when prompted

3. **Verify Installation**
   ```bash
   conda --version
   python --version
   ```

## 🛠️ Development Environment Setup

### Option 1: Visual Studio Code (Recommended)

#### Installation
1. **Download VS Code**
   - Visit [code.visualstudio.com](https://code.visualstudio.com)
   - Download for your operating system
   - Install following the wizard

2. **Essential Extensions**
   ```
   Install these extensions:
   📦 Python (by Microsoft)
   📦 Python Docstring Generator
   📦 Pylance
   📦 Code Runner
   📦 GitLens
   📦 Bracket Pair Colorizer
   📦 indent-rainbow
   📦 Material Icon Theme
   ```

3. **Python Extension Configuration**
   ```json
   // settings.json
   {
       "python.defaultInterpreterPath": "python",
       "python.linting.enabled": true,
       "python.linting.pylintEnabled": true,
       "python.formatting.provider": "black",
       "python.linting.flake8Enabled": true,
       "editor.formatOnSave": true
   }
   ```

#### VS Code Setup for DSA
```json
// Launch configuration for debugging
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python: Current File",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal",
            "args": []
        },
        {
            "name": "Python: Test File",
            "type": "python",
            "request": "launch",
            "module": "pytest",
            "args": ["${file}"],
            "console": "integratedTerminal"
        }
    ]
}
```

### Option 2: PyCharm

#### Community Edition (Free)
1. **Download PyCharm**
   - Visit [jetbrains.com/pycharm](https://www.jetbrains.com/pycharm/)
   - Download Community Edition
   - Install following the wizard

2. **Configuration**
   - Create new project
   - Select Python interpreter
   - Configure code style to PEP 8

### Option 3: Jupyter Notebook
Perfect for interactive learning and experimentation.

#### Installation
```bash
# Using pip
pip install jupyter

# Using conda
conda install jupyter

# Start Jupyter
jupyter notebook
```

#### JupyterLab (Enhanced Interface)
```bash
# Install JupyterLab
pip install jupyterlab

# Start JupyterLab
jupyter lab
```

## 📦 Essential Packages Installation

### Core Development Packages
```bash
# Code formatting and linting
pip install black flake8 pylint

# Testing framework
pip install pytest pytest-cov

# Documentation
pip install sphinx

# Performance profiling
pip install memory-profiler line-profiler
```

### Data Structures and Algorithms Packages
```bash
# Numerical computing
pip install numpy

# Data manipulation
pip install pandas

# Visualization
pip install matplotlib seaborn

# Graph algorithms
pip install networkx

# Algorithm visualization
pip install matplotlib pygame
```

### Complete Installation Script
Create a file named `setup_environment.py`:

```python
#!/usr/bin/env python3
"""
Environment setup script for Python DSA course
"""

import subprocess
import sys

def install_package(package):
    """Install a package using pip"""
    try:
        subprocess.check_call([sys.executable, "-m", "pip", "install", package])
        print(f"✅ Successfully installed {package}")
    except subprocess.CalledProcessError:
        print(f"❌ Failed to install {package}")

def main():
    packages = [
        # Core development
        "black", "flake8", "pylint", "pytest", "pytest-cov",
        # Data science
        "numpy", "pandas", "matplotlib", "seaborn",
        # Algorithms
        "networkx", "graphviz",
        # Utilities
        "tqdm", "colorama", "tabulate",
        # Profiling
        "memory-profiler", "line-profiler"
    ]
    
    print("🚀 Installing Python packages for DSA course...")
    for package in packages:
        install_package(package)
    
    print("\n🎉 Environment setup complete!")
    print("Run 'python --version' to verify your installation.")

if __name__ == "__main__":
    main()
```

Run the setup script:
```bash
python setup_environment.py
```

## 🔍 Environment Verification

### Create Verification Script
```python
# verify_setup.py
import sys
import pkg_resources

def check_python_version():
    """Check Python version"""
    version = sys.version_info
    if version.major == 3 and version.minor >= 8:
        print(f"✅ Python {version.major}.{version.minor}.{version.micro} - OK")
        return True
    else:
        print(f"❌ Python version {version.major}.{version.minor} - Upgrade needed")
        return False

def check_packages():
    """Check if required packages are installed"""
    required_packages = [
        'numpy', 'matplotlib', 'pytest', 'black', 'networkx'
    ]
    
    missing_packages = []
    for package in required_packages:
        try:
            pkg_resources.get_distribution(package)
            print(f"✅ {package} - Installed")
        except pkg_resources.DistributionNotFound:
            print(f"❌ {package} - Missing")
            missing_packages.append(package)
    
    return len(missing_packages) == 0

def main():
    print("🔍 Verifying Python DSA Environment Setup\n")
    
    python_ok = check_python_version()
    packages_ok = check_packages()
    
    print("\n" + "="*50)
    if python_ok and packages_ok:
        print("🎉 Environment setup is complete and ready!")
        print("You can now start the Python DSA course.")
    else:
        print("⚠️  Environment setup needs attention.")
        print("Please install missing components before proceeding.")

if __name__ == "__main__":
    main()
```

## 🗂️ Project Structure Setup

### Create Course Directory Structure
```python
# create_structure.py
import os

def create_directory_structure():
    """Create the complete course directory structure"""
    
    directories = [
        "projects",
        "practice/daily",
        "practice/topic-wise",
        "solutions/hackerrank",
        "solutions/leetcode",
        "notes",
        "tests",
        "utilities",
        "data",
        "visualizations"
    ]
    
    for directory in directories:
        os.makedirs(directory, exist_ok=True)
        print(f"📁 Created: {directory}")
    
    # Create initial files
    files_to_create = {
        "practice/daily/README.md": "# Daily Practice Problems\n\nTrack your daily coding practice here.",
        "notes/learning_log.md": "# Learning Log\n\nDocument your learning journey here.",
        ".gitignore": """
# Python
__pycache__/
*.py[cod]
*$py.class
*.so
.Python
env/
venv/
ENV/

# IDEs
.vscode/
.idea/
*.swp
*.swo

# OS
.DS_Store
Thumbs.db

# Project specific
data/temp/
*.log
""",
        "config.py": """
# Configuration file for Python DSA course

# Paths
DATA_DIR = "data"
SOLUTIONS_DIR = "solutions"
PRACTICE_DIR = "practice"

# Settings
DEBUG_MODE = True
VISUALIZATION_ENABLED = True
PROFILING_ENABLED = False

# Platform URLs
HACKERRANK_URL = "https://www.hackerrank.com"
LEETCODE_URL = "https://leetcode.com"
"""
    }
    
    for file_path, content in files_to_create.items():
        with open(file_path, 'w') as f:
            f.write(content)
        print(f"📄 Created: {file_path}")

if __name__ == "__main__":
    create_directory_structure()
    print("\n🎉 Project structure created successfully!")
```

## ⚡ Quick Start Guide

### Daily Development Workflow
1. **Start Your Day**
   ```bash
   # Activate virtual environment (if using)
   python -m venv dsa_env
   source dsa_env/bin/activate  # Linux/Mac
   dsa_env\Scripts\activate     # Windows
   
   # Update packages if needed
   pip install --upgrade pip
   ```

2. **Coding Session**
   ```bash
   # Open your IDE
   code .  # VS Code
   # or
   pycharm .  # PyCharm
   
   # Run tests
   pytest tests/
   
   # Format code
   black your_file.py
   
   # Check code quality
   flake8 your_file.py
   ```

3. **End of Session**
   ```bash
   # Commit your progress
   git add .
   git commit -m "Completed topic: [topic_name]"
   
   # Update learning log
   # Document what you learned today
   ```

## 🔧 Troubleshooting Common Issues

### Python Not Found
**Problem**: `python` command not recognized
**Solution**:
```bash
# Windows: Add Python to PATH
# Linux/Mac: Use python3 instead of python
python3 --version
```

### Package Installation Fails
**Problem**: pip install fails with permission errors
**Solution**:
```bash
# Use --user flag
pip install --user package_name

# Or use virtual environment
python -m venv myenv
source myenv/bin/activate  # Linux/Mac
pip install package_name
```

### VS Code Python Extension Issues
**Problem**: Python extension not detecting interpreter
**Solution**:
1. Press `Ctrl+Shift+P` (Cmd+Shift+P on Mac)
2. Type "Python: Select Interpreter"
3. Choose the correct Python installation

### Import Errors
**Problem**: "ModuleNotFoundError" when importing packages
**Solution**:
```bash
# Verify package installation
pip list | grep package_name

# Reinstall package
pip uninstall package_name
pip install package_name

# Check Python path
python -c "import sys; print(sys.path)"
```

## 📚 Next Steps

After completing the environment setup:

1. **✅ Verify Installation**: Run the verification script
2. **📁 Create Project Structure**: Use the structure creation script
3. **🔧 Configure IDE**: Set up your preferred development environment
4. **📖 Start Learning**: Proceed to [Python Syntax and Indentation](./02-syntax-indentation.md)

## 🎯 Success Checklist

- [ ] Python 3.8+ installed and accessible
- [ ] IDE/Editor configured with Python support
- [ ] Essential packages installed
- [ ] Project structure created
- [ ] Environment verification script passes
- [ ] First Python program runs successfully

**Congratulations!** 🎉 You now have a complete Python development environment ready for your data structures and algorithms journey!
