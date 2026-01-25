---
title: Python
description: This doc page covers tips and tricks you can use with python.
icon: fontawesome/brands/python
---

# Python Tips and Tricks

### Setting up a virtual environment
!!! Info
    Ensure you have python installed for this to work -> 
    [Download Python here](https://www.python.org/downloads/) 

    === "Windows"
        ``` bash
        mkdir {dir_name}
        cd {dir_name}
        py -3 -m venv env
        env\scripts\activate
        ```
    === "Mac/Linux"
        ``` bash
        mkdir <{dir_name}>
        cd {dir_name}
        python3 -m venv venv
        source venv/bin/activate
        ```

### How to generate requirements files
``` bash
pip3 freeze > requirements.txt
```

### Fix pip env error 
``` bash
python -m pip install --upgrade pip
python -m pip install --upgrade --force-reinstall pip
```