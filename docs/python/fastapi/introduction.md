
## Basic program
```py title="fastapi set up" linenums="1" hl_lines="2-4"
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def root():
    return {"message": "Hello World"}

```

## To run 
- fastapi dev main.py
- fastapi run main.py 

## Routes  
@app.get()  
@app.post()  
@app.put()  
@app.delete()  
 
 
And the more exotic ones:   
  - @app.options().    
  - @app.head().   
  - @app.patch().   
  - @app.trace().   

https://www.youtube.com/watch?v=DeZjkCtttss
