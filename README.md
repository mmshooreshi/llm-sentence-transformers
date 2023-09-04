# llm-sentence-transformers

[![PyPI](https://img.shields.io/pypi/v/llm-sentence-transformers.svg)](https://pypi.org/project/llm-sentence-transformers/)
[![Changelog](https://img.shields.io/github/v/release/simonw/llm-sentence-transformers?include_prereleases&label=changelog)](https://github.com/simonw/llm-sentence-transformers/releases)
[![Tests](https://github.com/simonw/llm-sentence-transformers/workflows/Test/badge.svg)](https://github.com/simonw/llm-sentence-transformers/actions?query=workflow%3ATest)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](https://github.com/simonw/llm-sentence-transformers/blob/main/LICENSE)

[LLM](https://llm.datasette.io/) plugin for embedding models using [sentence-transformers](https://www.sbert.net/)

## Installation

Install this plugin in the same environment as LLM.
```bash
llm install llm-sentence-transformers
```
## Configuration

After installing the plugin you need to register one or more models in order to use it. The [all-MiniLM-L6-v2](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2) model is registered by default, and will be downloaded the first time you use it.

You can try that model out like this:

```bash
llm embed -m mini-l6 -c 'hello'
```
This will return a JSON array of floating point numbers.

You can add more models using the `llm sentence-transformers register` command. Here is a [list of available models](https://www.sbert.net/docs/pretrained_models.html).

Two good models to start experimenting with are `all-MiniLM-L12-v2` - a 120MB download - and `all-mpnet-base-v2`, which is 420MB.

To install that [all-mpnet-base-v2](https://huggingface.co/sentence-transformers/all-mpnet-base-v2) model, run:

```bash
llm sentence-transformers register \
  all-mpnet-base-v2 \
  --alias mpnet
```
The `--alias` is optional, but can be used to configure one or more shorter aliases for the model.

You can run `llm aliases` to confirm which aliases you have configured, and [llm aliases set](https://llm.datasette.io/en/stable/aliases.html) to configure further aliases.

## Usage

Once you have installed an embedding model you can use it like this:

```bash
llm -m sentence-transformers/all-mpnet-base-v2 \
  -c "Hello world"
```
Or use its alias:
```bash
llm -m mpnet -c "Hello world"
```
Embeddings are more useful if you store them in a database - see [the LLM documentation](https://llm.datasette.io/en/stable/embeddings/cli.html#storing-embeddings-in-sqlite) for instructions on doing that.

## Development

To set up this plugin locally, first checkout the code. Then create a new virtual environment:
```bash
cd llm-sentence-transformers
python3 -m venv venv
source venv/bin/activate
```
Now install the dependencies and test dependencies:
```bash
pip install -e '.[test]'
```
To run the tests:
```bash
pytest
```
