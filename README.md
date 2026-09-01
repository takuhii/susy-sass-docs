Power Tools For The Web
=======================

Susy-SASS is an agnostic set of tools
for creating powerful, custom layouts.
We provide the language,
but you provide all the opinions.
Use a grid, don't use a grid,
or use a combination of grids —
it's all up to you.

We didn't want to build another system,
we wanted to build power tools
that you could use in any system.

Your markup, your layout | *our math*

Resources
---------

- [Website](http://takuhii.github.io/susy-sass/)
- [Documentation](https://susy-sass-docs.readthedocs.io/en/latest/)

Building the docs locally
-------------------------

The documentation is built with [Sphinx](https://www.sphinx-doc.org/). The
pinned toolchain lives in `docs/requirements.txt` and requires Python 3.12+.

Use a virtual environment so the docs toolchain stays isolated from your global
Python (this avoids picking up an older, incompatible Sphinx):

```bash
# create and activate a virtual environment
python3 -m venv .venv
source .venv/bin/activate

# install the pinned docs dependencies
pip install -r docs/requirements.txt

# build the HTML docs into docs/_build/html
npm run docs
# or, equivalently:
# sphinx-build -b html docs docs/_build/html
```

Then open `docs/_build/html/index.html` in a browser. The `docs/_build/`
directory is generated output and is git-ignored.

Read the Docs builds the same way automatically on each push, using the
Python version and requirements declared in `.readthedocs.yaml`.
