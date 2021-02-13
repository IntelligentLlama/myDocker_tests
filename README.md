# myDocker_tests
....Docker related exercises to test Docker image for Python:

## High level instructions:

### 1) create a new directory in your local machine to hold the new files
    ... $ mkdir my-app-5
    
### 2) Download files index.py and requirements.txt on the directory created
    .... file sample index .py
    from flask import Flask
    app = Flask(__name__)
    @app.route("/")
    def hello():
          return "Hello World!"
    if __name__ == "__main__":
            app.run(host="0.0.0.0", port=int("5000"), debug=True)

### 3) Download Docker file or create one:
   .... sample output:
   
   FROM python:alpine3.7
   COPY . /app
   WORKDIR /app
   RUN pip install -r requirements.txt
   EXPOSE 5000
   CMD python ./index.py

### 4) Build docker image in your machine terminal in the directory created in step 1: $ docker build --tag my-python-app-5 .
    .... sample output:
    
    $ docker build --tag my-python-app-5
    ...
    ....
    => [2/4] COPY . /app                                                                                                                                                0.1s
    => [3/4] WORKDIR /app                                                                                                                                               0.0s
    => [4/4] RUN pip install -r requirements.txt                                                                                                                        3.5s
    => exporting to image                                                                                                                                               0.1s
    => => exporting layers                                                                                                                                              0.1s
    => => writing image sha256:f0e3dc181a7bf01245ae3570f2bb17a1d3be6a14fbdf3b661a002e827cd0ae1c                                                                         0.0s
    => => naming to docker.io/library/my-python-app-5
 
### 5) Validate image: $ docker images
    ... sample output
    
    $ docker images
    REPOSITORY                      TAG       IMAGE ID       CREATED              SIZE
    my-python-app-5                 latest    f0e3dc181a7b   About a minute ago   91.6MB

### 6) Run/create the Docker container: $ docker run --name python-app -p 5000:5000 my-python-app-5
    ... sample output:
    
    docker run --name python-app -p 5000:5000 -d my-python-app-5
    * Serving Flask app "index" (lazy loading)
    * Environment: production
        WARNING: This is a development server. Do not use it in a production deployment.
        Use a production WSGI server instead.
    * Debug mode: on
    * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
    * Restarting with stat
    * Debugger is active!
    * Debugger PIN: 280-157-401
   
### 7) Test in your browser: locahost:5000
   ... you will see a Hello World! message
