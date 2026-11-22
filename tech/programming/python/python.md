# Python

## Install/upgrade pip for a custom (non-system) python

Also upgrade typing-extensions to fix black formatter crash

```bash
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt-get update
sudo apt-get upgrade
sudo apt install python3.15 python3.15-dev python3.15-venv
sudo python3.15 -m ensurepip --upgrade
sudo python3.15 -m pip install --upgrade typing-extensions
```

# Essential python packages
- pip
- pandas
