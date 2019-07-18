# Flask
Flask is a WSGI wrapper for creating simple servers.

## Installation
```bash
# Create an environment
$ mkdir myproject
$ cd myproject
$ python3 -m venv venv

# Start the environment
$ . venv/bin/activate

# Install Flask
```

## Hello World
```python
from flask import Flask

# This creates a WSGI application, and the argument we pass tells Flask where to look for static files
# If it were in a module, it would
app = Flask(__name__)

# The route decorator determines which route triggers the function
# The function name determines the URL for the function and returns the value to display
@app.route('/')
def hello_world():
    return 'Hello, World!'

```

## Running your app
```bash
$ env FLASK_APP=<FILE NAME HERE> flask run
```

## More documentation
[Quickstart](https://flask.palletsprojects.com/en/1.1.x/quickstart/)
[API](https://flask.palletsprojects.com/en/1.1.x/api/#)
