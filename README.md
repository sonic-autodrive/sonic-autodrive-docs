Template for the Read the Docs tutorial
=======================================

This GitHub template includes fictional Python library
with some basic Sphinx docs.

Read the tutorial here:

https://docs.readthedocs.io/en/stable/tutorial/

# Sphinxを使ってMarkdownで書きたい場合

```
<feature/markdown-supportブランチにチェックアウト>

pip install -r docs/requirements.txt

cd docs

make html

<buildディレクトリが作成されるので、その中のindex.htmlにブラウザからアクセス>
```
