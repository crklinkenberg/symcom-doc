---
{"dg-publish":true,"permalink":"/topics/chapter-classification-python-guide/"}
---


# Medical Symptom Classification System

## System Prerequisites

- Have python3 installed
- Have the MySQL server set up. Check [README](./database/README.md).

## Running locally

From the upmost directory of the project run:

```bash
python -m pip install --upgrade pip
cd ./restServer
pip install -r requirements.txt
python -m nltk.downloader stopwords
python -m spacy download en_core_web_md
python -m spacy download de_core_news_md
uvicorn main:app
```

After running the image you may navigate to
[`127.0.0.1:8000/docs`](http://127.0.0.1:8000/docs) to view the Swagger endpoint and investigate the available endpoints.

## Running locally with Docker image

Make sure your port 8000 is open and available. To do so:

```bash
cd ./restServer
ufw allow 8000
docker compose up -d --build
```

After running the image you may navigate to
[`127.0.0.1:8000/docs`](http://127.0.0.1:8000/docs) to view the Swagger endpoint and investigate the available endpoints.

## Automated Testing

[Automated tests](./restServer/dataProcessing/tests/) can be run as any other individual file. Example:

```bash
python -m restServer.dataProcessing.tests.buildTree0Test
```

This command needs to be called from within the repository's top directory, i.e.: "./restServer".

## Run Individual Files

Files (except tests) are not designed to display any output. But, they can be individually 'ran' using:

```bash
python -m package.subpackge.file
```

This command needs to be called from within the repository's top directory, i.e.: "./restServer".

For further documentation check the [documentation](./documentation) directory
