---
layout: post
title:  "PwC JAcademy Volume 5 Kickoff"
categories: jacademy
published: true
---


# Getting started with python

## Goals

- Verify python is up and running
- Prepare project directory and virtual environment
- Set up a FastAPI python project
- Run the server
- Test the application with Swagger UI
- Test the application with visual studio plugin
- Prepare proof-of-concept from employees application endpoints

## Verify python is up and running

We can to make sure that we have python installed, and we are in the correct version.
We want to use 3.14 (**π**ython :)).

To check for our python version, we want to run the following command:
```bash
python3 -V
```

- Whenever we use terminal command, we will be using bash (git bash for windows users).
- Bash is strict on capitals, make sure you write -V and not -v.
- If you somehow end up in a python terminal, type exit to return.

## Prepare project directory and virtual environment

Our next steps is to create a directory/folder for our new project, and then set up the virtual environment.

Create the directory somewhere where you can have easy access to. Since we will use multiple repositories eventually, we should plan ahead.
A proposed directory structure is the following:
```
{yourPath}/academy
{yourPath}/academy/python-backend
```
<hr>

Next we need to create our virtual environment for our application.
But what is this virtual environment?
[Virtual Environment official documentation](https://docs.python.org/3/library/venv.html)

You can (and should) read the docs about it. But essential it's a way to have multiple projects with different configurations (and without breaking your other projects).

To create the necessary files we run the following command (after we navigate to the new project directory!):
```bash
python3 -m venv .
```

The dot (.) in the command tells it to create the files where we are. We could instead use a name there, which would create a new folder with all the files inside, but we already prepared the directory in the previous step.

<hr>

Finally, we want to activate the venv.
To do so, we need to run the following command, from the project directory:
```bash
source myfirstproject/bin/activate
```

To verify which venv you are running, you can run the following command:
```bash
which python
```

*You can later disable your virtual env with `$ deactivate`*

## Set up a FastAPI python project

What is FastAPI, and why do we need it?
[FastAPI official page](https://fastapi.tiangolo.com/)

*The official page is a great way to also learn the library properly and in depth. Documentation is very decent!*

To use FastAPI, we need to set up the dependency for it and then prepare out initial python file.

### Dependency management

While you can simply run pip instal for everything, eventually you will run in issues where you don't know what you have installed and it's very hard to replicate your project setup. So we also need a way to track our dependencies.

#### First we want to instal FastAPI as a dependency

```bash 
pip install "fastapi[standard]"
```

#### Create requirements.txt file
Next we want to "freeze" our dependencies for now. To do so we run the following command:

```bash 
pip freeze > requirements.txt
```

Running the above command will create a new file, with all dependencies. This is useful since we want to be able to replicate the exact application on multiple computers eventually.

If we want to instal all dependencies from the `requirements.txt` file, we can use the following command (*no need to run it now though*):
```bash
pip install -r requirements.txt
```


#### Add main\.py

Time to write some python!

In our root directory, create a new file called main.py and inside copy paste the following code (this is the example from the official docs)

```python
from typing import Union

from fastapi import FastAPI

app = FastAPI()


@app.get("/")
def read_root():
    return {"Hello": "World"}


@app.get("/items/{item_id}")
def read_item(item_id: int, q: Union[str, None] = None):
    return {"item_id": item_id, "q": q}
```

For now we will keep the simplest example and then modify it for our target application.

## Run the server

To run the server you need to run the following command:

```bash
fastapi dev main.py
```
Assuming everything went well, you should be able to see the server running in the terminal, and 2 urls to access the server.
Try pressing them with `ctrl/cmd + click` in the terminal.

## Test the application with Swagger UI

### Accessing docs and testing available endpoints
By accessing the docs url (it should be `http://127.0.0.1:8000/docs`), you can see all endpoints currently available and try them out.

Currently the application doesn't really do anything useful, apart from the two get services.

Try out the `/items/{item_id}` endpoint, see how it responds to your values.

### Adding a new endpoint
Next, we want to add a new endpoint and see how difficult it is to try out new code!

Add the following code in our main.py, while the server it's still running!
```python
@app.get("/academy")
def read_academy():
    return "Patras Software Academy!"
```
Afterwards, refresh the docs page and you will see the new endpoint available for testing.

## Test the application with visual studio plugin

Testing the server with the docs page will become tiresome very quickly.
There are many tools to make calling server endpoints easier, with the most famous being [Postman](https://www.postman.com/).

For our sessions, we will use a different tool, which can be used through VSC:
**REST Client**

### Calling the application with Rest Client plugin

1) First we need to create a new file with the name `requests.http`
2) Add the following code in the file
```http
# Hello world
GET http://localhost:8000
```
3) Press the `Send request`


## Prepare proof-of-concept from employees application endpoints

For our react application, we will need the following endpoints and http actions:
`/api/v1/employees GET`
`/api/v1/employees POST`
`/api/v1/employees/{id} GET`
`/api/v1/employees/{id} PUT`
`/api/v1/employees/{id} DELETE`

For now, we will keep the application in just a single file, ignoring most of the established "good practices".
Copy and paste the following code in the main.py:

```python
# Employees mocking 
class Employee(BaseModel):
    id: int
    firstName: str
    lastName: str
    email: str

all_employees = [Employee(id=1, firstName="George", lastName="Mammos", email="giorgos.mammos@pwcacademy.gr"),
            Employee(id =2, firstName="Stella", lastName="Vlassi", email="stella.vlassi@pwcacademy.gr")]


# `/api/v1/employees GET`
@app.get("/api/v1/employees") 
def get_employees() -> list[Employee]:
    return all_employees


# `/api/v1/employees POST`
@app.post("/api/v1/employees")
def post_employees(employee: Employee):
    all_employees.append(employee)


# `/api/v1/employees/{id} GET`
@app.get("/api/v1/employees/{id}")
def get_employee_by_id(id:int) -> Employee:
    for employee in all_employees:
        if employee.id == id:
            return employee

# `/api/v1/employees/{id} PUT`
@app.put("/api/v1/employees/{id}")
def put_employee_by_id(new_employee_data: Employee) -> Employee:
    for employee in all_employees:
        if employee.id == new_employee_data.id:
            employee.firstName = new_employee_data.firstName
            employee.lastName = new_employee_data.lastName
            employee.email = new_employee_data.email
            return employee

# `/api/v1/employees/{id} DELETE`
@app.delete("/api/v1/employees/{id}")
def delete_employee_by_id(id:int) :
    for index, employee  in enumerate(all_employees):
        if employee.id == id:
            index_of_employee_to_delete = index
    
    del(all_employees[index_of_employee_to_delete])
```

## Reading material
- [Swagger specification](https://swagger.io/specification/)
- [FastAPI features](https://fastapi.tiangolo.com/features/#fastapi-features)
- [HTTP request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods)

