# Elvis Has Left the Building
A Jupyter notebook extension for interactive code generation and experimentation. Elvis helps you track and reproduce your exploratory coding sessions by generating editable code cells from templates. Perfect for:
- Saving exact object recreation code
- Working in terminals where copy-paste is painful
- Quick templating of repetitive code
  
Some say it's pointless. Some say it's brilliant. Elvis doesn't care either way - Elvis has already left the building.

## Key Features
* Creates editable Jupyter cells with your generated code
* Perfect for data analysis exploration where you try different parameters
* Remembers variables between templates to track your working combinations
* Helps recreate your exact setup after notebook restarts or crashes

## Install
```bash
pip install elvis-repl
```

## Usage
```python
from elvis_repl import elvis

# Define your template with parameters
elvis("df = pd.read_csv(\"{file}\", skiprows={skip})", 
      file="data.csv", skip=2)

# Use .show() to create an editable cell with the generated code
elvis.show()
# Creates a new cell with:
# df = pd.read_csv("data.csv", skiprows=2)

# Experiment with different parameters
elvis._vars['skip'] = 3
elvis.show()  # Creates another editable cell with updated code

# When you're happy with the result, you can run it
elvis.run()  # Executes the code

# Also useful for generating multiple configurations
configs = [{"host": "db1", "port": 5432}, {"host": "db2", "port": 5433}]
for cfg in configs:
    elvis("conn_{host} = connect(host='{host}', port={port})", **cfg)
    elvis.show()  # Creates a new cell for each configuration
```

## Why Elvis?
* Interactive Exploration: Perfect for data analysis where you're trying different parameters and want to save what worked
* Session Recovery: When your Jupyter kernel crashes, Elvis helps you recreate everything exactly as it was
* Code Generation: Easily create multiple similar code blocks with different parameters
* Works in CLI too: Falls back to printing code in terminal environments

Remember: Elvis helps you track how you built things, so when your Jupyter session leaves the building, you know exactly how to bring it back.
Note: While Elvis works in regular Python terminals, its main strength is the Jupyter integration where it creates editable code cells.

Remember: When your session crashes, Elvis makes sure you know how to rebuild everything exactly as it was.
