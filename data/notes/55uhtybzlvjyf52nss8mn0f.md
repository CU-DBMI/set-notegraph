
## Summary

The following note covers how to create Dendron-compatible notes from Jupyter notebook files.

- Jupyter notebooks are JSON files used to compose markdown and code intended to be executed within specialized notebook-compatible environments.
- Dendron notes are markdown files with frontmatter.
- Jupytext may be used to create Markdown files from Jupyter notebooks.

## Process

1. Begin with a Jupyter notebook file
1. Install [Jupytext](https://jupytext.readthedocs.io/en/latest/)
1. [Pair Jupyter notebook file with markdown file](https://jupytext.readthedocs.io/en/latest/paired-notebooks.html)
1. Apply [Dendron Doctor: fixFrontMatter](https://wiki.dendron.so/notes/ZeC74FYVECsf9bpyngVMU/#fixfrontmatter) to resulting markdown file.
1. Enjoy the Jupyter notebook as a Dendron note ✅

Special notes:

- Output from Jupyter notebook cells are not saved by Jupytext when converting to markdown.
- Each time the notebook is saved, Jupytext pairing will overwrite the Dendron-compatible frontmatter within the markdown file.
- Despite this, Dendron Doctor: fixFrontMatter appears to be able to retain the note ID.
