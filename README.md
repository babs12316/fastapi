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



# Middelware

If you have multiple endpoints and you want the same logic to run for every request, middleware makes sense.

If you have only one endpoint with one function, it’s better to put the logic directly inside that function instead of middleware.

request.body is stream so once read it becomes empty


```
@app.middleware("http")
async def log_requests(request: Request, call_next):
    start = time.time()
    response = await call_next(request)
    duration = time.time() - start

    print(f"{request.method} {request.url.path} → {duration:.2f}s")
    return response


Registers a global HTTP middleware
Runs before and after every request.

request: Request  
Gives you access to:
path (/chat)
method (POST)
headers
body

call_next(request)
you have handled request now what to do? this call_next function pass response of middelware to route (POST /chat)  or next middelware
```

Middelware should be used for   
Logging & observability (most common) like shown in above example
Authentication / authorization (headers-based)
```
auth = request.headers.get("Authorization")
```
Rate limiting  
```
client_ip = request.client.host

```
CORS / security headers  
```
response.headers["X-Frame-Options"] = "DENY"

```
Global request blocking (path / method)
```
if request.url.path.startswith("/admin"):
    return JSONResponse(status_code=403)

```


Python modules expose everything by default.  


# use of __all__  
```
# app.py
from fastapi import FastAPI

app = FastAPI()

__all__ = ["app"]  -->  If someone uses from app import *, only give them app
```





# test function  
def test_health():  
Any function starting with test_ is a test

```
from fastapi.testclient import TestClient
from api import app

client = TestClient(app)

def test_health():
    response = client.get("/health")
    assert response.status_code == 200
    assert response.json()["status"] == "ok"


```


<img width="793" height="335" alt="Screenshot 2026-02-04 at 22 34 40" src="https://github.com/user-attachments/assets/095b19d9-dc9c-4f5e-b6a6-728ffb60170a" />     
    
<img width="950" height="633" alt="Screenshot 2026-02-04 at 22 46 17" src="https://github.com/user-attachments/assets/dbfd960a-96a7-44e5-a7d5-970e4a9140bc" />  
 

<img width="918" height="426" alt="Screenshot 2026-02-04 at 22 47 15" src="https://github.com/user-attachments/assets/fe213dc7-5fa9-4e97-b102-afe9afd47ed8" />  
  


 <img width="712" height="539" alt="Screenshot 2026-02-04 at 23 04 57" src="https://github.com/user-attachments/assets/9f891977-ba5f-4e94-a844-e0ec52ace8f1" />

  
 <img width="850" height="627" alt="Screenshot 2026-02-04 at 23 05 52" src="https://github.com/user-attachments/assets/0c2dad9d-437d-461a-b83e-c06ff9def2a3" />


