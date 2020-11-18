First try on a full documentation Pipeline
==========================================

## Setup

Breaking it down:

* The action is triggered on push to the master branch. Generally you should be pushing most commits to other branches anyways, so this action should only run occasionally when the main code branch is updated. Those commented out lines can be used to disable the action.
* Requirements: Some stuff comes pre-installed on the image, some doesn’t. Luckily brew and pip do, but doxygen and sphinx and such — well you are on your own! The complete list of pre-installed software is here. Note that we used pip3 for python3.
* Checkout repo: An important step. This didn’t use to be required, but now it is (*sigh*) so beware!
* Build docs: This builds the docs just like before, with one very important addition:
* GitHub pages uses Jekyll to build it’s websites, which ignores directories that start with a _. This is a problem because many of the files we care about like .js and .css files are in the_static folder. The easy workaround is to disable Jekyll entirely with the lines:


.. code-block:: bash
{
…
&& cd _build/html
&& touch .nojekyll
}


Deploy: This deploys the docs_sphinx/_build/html folder.
Add it to the `git` repo and push:

```
git add .github
git commit -m “Docs”
git push

```
