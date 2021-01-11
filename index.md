## Bootstrap Flask Application 
[Flask](https://flask.palletsprojects.com/en/1.1.x/) è molto facile da usare per creare REST API con [Python](https://www.python.org/) leggere, anche con un singolo file. Questo repository è un template per cominciare a sviluppare applicazione più complesse con Flask.

**bootstrap-flask** è un [repository template](https://docs.github.com/en/free-pro-team@latest/github/creating-cloning-and-archiving-repositories/creating-a-repository-from-a-template) da cui si può partite per creare altri repository.

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

### Run 

```
$ git clone https://github.com/gzileni/flask-bootstrap.git
$ cd flask-bootstrap
$ pip install -r requirements.txt
$ export FLASK_APP=main.py
$ flask run
```

## Docker 
Un modo semplice per eseguire e condividere l'applicazione con il team e inviarlo alla produzione è utilizzando [Docker](https://docs.docker.com/install/).

```
$ docker build -t flask-bootstrap .
$ docker run -p 5000:5000 flask-bootstrap
$ docker container list
```
