# fastapi

Think of BaseModel as:  

A smart data container that:  

1. validates data  
ChatRequest(message=123)
value is not a valid string

2. converts types  
ChatRequest(message=42)
message = "42"


3. errors cleanly if data is wrong  
ChatRequest()
Field required: message


Pydantic is a data validation and parsing library for Python.  

It answers this question:  
 
“How do I safely turn untrusted data (JSON, user input, API requests) into correct Python objects?”  

The problem Pydantic solves

Imagine this data comes from the internet (React, curl, mobile app):

In Python, raw input is:

Untrusted

Typeless

Easy to break your app

Without Pydantic, you must manually:

Parse JSON

Check fields exist

Check types

Handle errors

Pydantic automates all of this.


What Pydantic gives you
1️⃣ Data validation

from pydantic import BaseModel

class ChatRequest(BaseModel):
    message: str

If someone sends:

{ "message": 123 }

Pydantic:

Detects wrong type

Raises a clean validation error

FastAPI converts it to HTTP 422

No crashes. No KeyError.

Type safety (at runtime)

Python normally does not enforce types.

Pydantic does.

This is huge for APIs.

Pydantic is a Python library that enforces data structure defined in classes, validates input at runtime, and converts it into safe Python objects.

# Python class inheritance

class Child(Parent):    
    
it means:

“Create a new class called Child that inherits everything from Parent i.e child extends parent”

Inheritance means:

The child class automatically gets all methods and behavior of the parent

The child can add new fields

The child can override behavior


class ChatRequest(BaseModel):
   message: str


ChatRquest extends all metods from BaseModel. But these methods (regarding validation, typecast, typecheck) are called by fastapi. we dont need to call them explicitly.

# Fastapi class  
from fastapi import FastAPI  
fastapi is class that provides all functionality for your api

app = FastAPI()

create a FastAPI "instance"

Here the app variable will be an "instance" of the class FastAPI.

This will be the main point of interaction to create all your API.
