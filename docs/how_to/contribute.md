# Contributing to GluonCV

Gluon-vision-toolkit has been developed by community members.
Everyone is more than welcome to contribute.
It is a way to make the project better and more accessible to more users.

## Guidelines
* [Submit Pull Request](#submit-pull-request)
* [Git Workflow Howtos](#git-workflow-howtos)
  - [How to resolve conflict with master](#how-to-resolve-conflict-with-master)
  - [How to combine multiple commits into one](#how-to-combine-multiple-commits-into-one)
  - [What is the consequence of force push](#what-is-the-consequence-of-force-push)
* [Document](#document)
* [Testcases](#testcases)
* [Examples](#examples)
* [Core Library](#core-library)
* [Python Package](#python-package)

## Submit Pull Request
* Before submitting, please rebase your code on latest master branch. You can do it with

```bash
git remote add upstream https://github.com/dmlc/gluon-cv
git fetch upstream
git rebase upstream/master
```
* If you have multiple small commits,
  it might be good to merge them together (use git rebase then squash) into more meaningful groups.
* Send the pull request!
  - Fix the problems reported by automatic checks
  - If you are contributing a new module or new function, add a test.

## Git Workflow Howtos
### How to resolve conflict with master
- First rebase to most recent master
```bash
# The first two steps can be skipped after you do it once.
git remote add upstream https://github.com/dmlc/gluon-cv
git fetch upstream
git rebase upstream/master
```
- The git may show some conflicts it cannot merge, say ```conflicted.py```.
  - Manually modify the file to resolve the conflict.
  - After you resolved the conflict, mark it as resolved by
```bash
git add conflicted.py
```
- Then you can continue rebase by
```bash
git rebase --continue
```
- Finally push to your fork, you may need to force push here.
```bash
git push --force
```

### How to combine multiple commits into one
Sometimes we want to combine multiple commits, especially when later commits are only fixes to previous ones,
to create a PR with set of meaningful commits. You can do it by following steps.
- Before doing so, configure the default editor of git if you haven't done so before.
```bash
git config core.editor the-editor-you-like
```
- Assume we want to merge last 3 commits, type the following commands
```bash
git rebase -i HEAD~3
```
- It will pop up an text editor. Set the first commit as ```pick```, and change later ones to ```squash```.
- After you saved the file, it will pop up another text editor to ask you modify the combined commit message.
- Push the changes to your fork, you need to force push.
```bash
git push --force
```

### Reset to the most recent master
You can always use git reset to reset your version to the most recent master.
Note that all your ***local changes will get lost***.
So only do it when you do not have local changes or when your pull request just get merged.
```bash
git reset --hard [hash tag of master]
git push --force
```

### What is the consequence of force push
The previous two tips requires force push, this is because we altered the path of the commits.
It is fine to force push to your own fork, as long as the commits changed are only yours.

## Testcases
- All the testcases are in tests

## Core Library
- Follow Google C style for C++.
- We use doxygen to document all the interface code.
- You can reproduce the linter checks by typing ```make lint```

## Python Package
- Always add docstring to the new functions in numpydoc format.
- You can reproduce the linter checks by typing ```make lint```

## Documentation
- Documentation of GluonCV is generated by sphinx that parses reStructuredText (reST) and CommonMark (Markdown) files.
  Parsing starts at the main index, `docs/index.rst`.
  - API documentation is generated from reST indices.
  - Examples in `docs/tutorials` are generated by Sphinx-Gallery to reST and referenced from the main index.
  - Plain, static documents are written in CommonMark and parsed with recommonmark bridge.
- A primer of reST is available from [sphinx](http://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html).
  - For basic syntax like inline markup, see [rst-cheetsheet from ralsina](https://github.com/ralsina/rst-cheatsheet/blob/master/rst-cheatsheet.rst).
  - To generate a special markup block, see [directives](http://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html#directives) and [Python directives](http://www.sphinx-doc.org/en/master/usage/restructuredtext/domains.html#the-python-domain).
  - __numpydoc__ docstrings, not reST docstrings, are used for API documentation in source code and parsed through sphinx.ext.napoleon.
    However, reST directives like [cross referencing Python objects](http://www.sphinx-doc.org/en/master/usage/restructuredtext/domains.html#cross-referencing-python-objects)
    or inserting a [doctest block](http://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html#doctest-blocks) is supported.
- A quick start of CommonMark is available at [Markdown Reference](https://commonmark.org/help/).
