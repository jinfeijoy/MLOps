## Automation 
* click: A Python package for building command line interfaces.
  ```
  import click

  @click.command()
  @click.argument('count', type=)
  @click.option('--count', default=1) # when run script in commend line, just add --count, the output will perform this function 
  def hello(count):
      for x in range(count):
          click.echo('Hello World!')
  
  if __name__ == '__main__':
      hello()
  ```
* ArgParse
  ```
  import argparse
  
  parser = argparse.ArgumentParser()
  parser.add_argument('--verbosity', action='store_true')
  args = parser.parse_args()
  
  if args.verbosity:
      print("Verbose mode enabled")
  ```
* sys.argv
  ```
  import sys 

  print(f"Script name: {sys.argv[0]}")
  print(f"First argument: {sys.argv[1]}") 
  print(f"Second argument: {sys.argv[2]}")
  ```
* Setuptools
  ```
  from setuptools import setup

  setup(
      name='mypackage',
      version='1.0',
      install_requires=['requests', 'click']
  )
  ```
* Entry points
  ```
  from setuptools import setup

  setup(
    #...,
    entry_points = {
      'console_scripts': [
        'myscript = mypackage.mymodule:main_func',
      ]  
    }
  )
  ```

# building ML API
* flash framework
```
from flask import Flask, abort

app = Flask(__name__)

@app.route('/')
def two_hundred():
  return "<h1> 200! all good </h1>'

@app.route('/error')
def error():
  abort(500, 'oooh some error!')

if __name__ == '__main__':
  app.run(debug=True, port=8000, host='0.0.0.0')

```
* [building an API with Flask](https://www.coursera.org/learn/python-mlops-duke/lecture/ZuUNp/building-an-api-with-flask)
```
from flask import Flask, request, jsonify
import torch
import numpy as np
from transformers import RobertaTokenizer
import onnxruntime

app = Flask(__name__)
tokenizer = RobertaTokenizer.from_pretrained('roberta-base')
session = onnxruntime.InferenceSession('roberta-sequence-classfication-09.onnx')

def to_numpy(tensor):
  return (
    tensor.detach().cpi.numpy() if tensor.requires_grad else tensor.cpu().numpy()
)

@app.route('/')
def home():
  return 'RoBERTa sentiment analysis'

@app.route('/predict', method = ['POST'])
def predict():
  input_ids = torch.tensor(
    tokenizer.encode(request.json[0], add_special_tokens=True)
  ).unsqueeze(
    0
  )
  inputs = {session.get_inputs()[0].name: to_numpy(input_ids)}
  out = session.run(None, inputs)

  result = np.argmax(out)
  return jsonify({'positive': bool(result)})

if __name__=='__main__':
  app.run(host='0.0.0.0', port=5000, debut=True)


# curl -X POST --header 'Content-Type: application/json' --data '['using curl is not to my liking'] http://127.0.0.1:5000/predict
```
* FastAPI: A Python web framework for building APIs.
  ```
  from fastapi import FastAPI

  app = FastAPI()
  
  @app.get("/")
  def read_root():
      return {"message": "Hello World"}
  
  print(read_root())
  ```
* Flask: A lightweight Python web framework.
  ```
  from flask import Flask

  app = Flask(__name__)
  
  @app.route("/")
  def home():
      return "Home Page"
  
  if __name__ == "__main__":
      app.run()
  ```
* Transforms: Hugging Face library for NLP tasks.
  ```
  from transformers import pipeline

  classifier = pipeline("sentiment-analysis")
  result = classifier("I love this course") 
  print(result)
  ```
* Onyx: ML model server for high-performance inferencing.
  ```
  import onnxruntime as rt

  sess = rt.InferenceSession("model.onnx")
  input_name = sess.get_inputs()[0].name
  res = sess.run(None, {input_name: x})
  ```
* OpenAPI: Specification for API documentation.
  ```
  from fastapi import FastAPI
  from fastapi.openapi.utils import get_openapi
  
  app = FastAPI()
  
  def custom_openapi():
      return get_openapi(
          title="Custom title",
          version="2.5.0",
          description="Custom description",
      )
      
  app.openapi = custom_openapi
  ```
