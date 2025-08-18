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
