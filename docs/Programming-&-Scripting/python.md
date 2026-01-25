icon: simple/python

## Setting up a virtual environment
!!! Note
    Ensure you have python installed for this to work. <br>
    [Download Python here](https://www.python.org/downloads/) 

    ### Windows
        ```
        mkdir <yourdir>
        cd <yourdir>
        py -3 -m venv env
        env\scripts\activate
        ```
    ### Mac / Linux
        ```
        mkdir <yourdir>
        cd <yourdir>
        python3 -m venv venv
        source venv/bin/activate
        ```

## Generate requirements files
```
pip3 freeze > requirements.txt
```

## Fix pip env error 
```
python -m pip install --upgrade pip
python -m pip install --upgrade --force-reinstall pip
```