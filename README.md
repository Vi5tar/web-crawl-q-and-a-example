# About
Modified source code for [How to build an AI that can answer questions about your website](https://platform.openai.com/docs/tutorials/web-qa-embeddings) tutorial.

The main changes are:
- file name convention
- exclude `.mp3`, `.pdf`, `.m4a` from being scraped
- use regex to determine reletive urls
- use regex to remove whitespace
- prepend the page url to it's text
- use `gpt-3.5-turbo` model
    - uses an updated version of `openai` python package
    - uses `openai.ChatCompletion.create` instead of `openai.Completion.create`

# Notes
Results were meh. It seems getting the right context on the fly for `gpt-3.5-turbo` is the crux of the problem.

> The question needs to be converted to an embedding with a simple function, now that the data is ready. This is important because the search with embeddings compares the vector of numbers (which was the conversion of the raw text) using cosine distance. The vectors are likely related and might be the answer to the question if they are close in cosine distance. The OpenAI python package has a built in distances_from_embeddings function which is useful here.
>
> https://platform.openai.com/docs/tutorials/web-qa-embeddings/building-a-question-answer-system-with-your-embeddings

The above didn't work as well as I had hoped. It required wording the question specific to the content in the page. Which requires pre-knowledge of the page. Which defeats the purpose of the exercise.

This contrived example produced the results I was looking for: https://github.com/compassion-technology/church-clippy-web/blob/main/app/api/chat/route.js

# Usage
Copy `.env.example` to `.env` and add your OpenAI API key.
```bash
cp .env.example .env
```
Setup a virtual environment and install dependencies.
```bash
python -m venv env

source env/bin/activate

pip install -r requirements.txt
```
Open the notebook.
```bash
jupyter notebook
```
