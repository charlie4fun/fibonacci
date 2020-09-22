# Fibonacci numbers
## What is it
It is a test task. RESTful service, which finds all the combinations of Fibonacci numbers that add up to a given number.

## Run
#### To run with docker-compose (recommended)
```bash
docker-compose up
```

#### To run locally:
```bash
python3 fib_app.py
```
I would also recommend to use [pyenv](https://github.com/pyenv/pyenv). It helps to manage Python versions and to avoid conflicts with system Python.

#### To create a docker image:
Docker container runs Python3 :) (which required additional adjustments in `Dockerfile`)
Image can be build:
```bash
docker build -t fibo-flask-app:latest .
```
and run (but in this case caching does not work):
```bash
docker run -d -p 5000:5000 fibo-flask-app
```

## Endpoints
1. /              - welcome page
2. /fib/<number>  - finds all the combinations of Fibonacci numbers that add up to a given number
3. /health        - healthcheck returns plain 200 response

## Architecture
Componenets:
1. Flask app
2. Redis cache

Flask app caches responses for `/fib/<number>` in Redis database.
Logs are redirected to stdout, where they could be picked up by most container orchestration tools, like K8s or ECS. 

## TODO:
Add gunicorn to container