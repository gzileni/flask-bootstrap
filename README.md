## Bootstrap Flask Application 
[Flask](https://flask.palletsprojects.com/en/1.1.x/) è molto facile da usare per creare REST API con [Python](https://www.python.org/) leggere, anche con un singolo file. Questo repository è un template per cominciare a sviluppare applicazione più complesse con Flask.

Cominciamo con il file di configurazione *config.py*:

```
class Config(object): 
    pass 
 
class ProdConfig(Config): 
    pass 
 
class DevConfig(Config): 
    DEBUG = True 
```

Il file principale *main.py* con gli ENDPOINT 
```
from flask import Flask 
from config import DevConfig 
 
app = Flask(__name__) 
app.config.from_object(DevConfig) 
 
@app.route('/') 
def home(): 
    return '<h1>Hello World!</h1>' 
 
if __name__ == '__main__': 
    app.run() 
```

Il template è un semplice Server REST API con un ENDPOINT '/' per visualizzare il classico "Hello World!" nel browser all'indirizzo to http://127.0.0.1:5000. 
Il progetto è strutturato in questo modo: 

```
Dockerfile          # Istruzioni per eseguire l'applicazione con Flask in un container docker 
requirements.txt    # Le dipendenze dell'applicazione
/venv               # Ambiente python viruale di sviluppo 
.gitignore          # Files da escludere nei commit per Git
main.py             # Il file principale
config.py           # La configurazione dell'applicazione
```

## Run 

```
$ export FLASK_APP=main.py
$ flask run
```

## Docker 
Un modo semplice per eseguire e condividere l'applicazione con il team e inviarlo alla produzione è utilizzando [Docker](https://docs.docker.com/install/).
One simple way to easily define and quickly spawn all these components is to use Docker containers. With Docker, you define all of your application components and how to install and configure them, and you can then share your stack with your team, and send it to production with the exact same specification.

## Run Docker containers 

```
$ docker build -t flask-bootstrap .
$ docker run -p 5000:5000 flask-bootstrap
$ docker container list
```