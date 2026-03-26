# set up venv
python3 -m venv venv

# start
source venv/bin/activate

# stop
deactivate

# packages
pip install mkdocs sets up package and is persisted until venv is deleted

# freeze
pip freeze > requirements.txt
rebuild with pip install -r requirements.txt