# Environment setup

This project uses python 3.9. The dependencies are managed with pip-tools.
To recreate the virtual environment:

1. Create virtual environment: `python -mvenv venv`
2. Activate it: `source venv/bin/activate`
3. Install `pip-tools`: `pip install pip-tools`
4. Install dependencies: `pip-sync`

During step 4 you might need to provide some external dependencies / activate modules on quest.

