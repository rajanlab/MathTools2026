# Mathematical Tools for Neuroscience contributing guide

This brief guide provides a few tips and guidelines for how to contribute to the Jupyterbook that contains most of the course material for Mathematical Tools for Neuroscience.

### Workflow for editing the course material

The Jupyterbook consists of a set of Jupyter notebooks (for videos and tutorials) and some Markdown pages (for overviews and key concepts) that contain the content of the course material.
The best way to work on these is to [create a local copy of the course repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) and then work on this local copy.
Pushing back changes to the main branch of the repository on Github causes the Jupyterbook, and so the course webpage, to rebuild.
This usually takes a while, and progress can be monitored in the actions tab of the repository.
Once building is complete, the changes should be reflected in the publically accessible webpage.

The best way to edit the course material is to build the Jupyterbook on your local machine before pushing it back to Github.
This ensures that all edits have the desired outcome before they affect the public-facing webpage.
How to do so is described in the next section.

### Building the course webpage locally

Once you have a local copy of the repository, you can build the Jupyterbook as follows.
First, install the required packages into a virtual environment (here assuming the use of the [uv package manager](https://docs.astral.sh/uv/)):
```Shell
uv venv --python 3.13
uv pip install -r requirements.txt
```
Once installed, the Jupyterbook is built by calling
```
uv run jupyter-book build .
```
Once completed, the course webpage will be available at `_build/html/index.html`.

Note that this will _not_ produce an exact copy of the course webpage, as it does not pre-process the Jupyter notebooks.
This is done to avoid modifying each of these files, which makes version control tricky.
In order to perform this pre-processing if desired, additionally run
```
uv run ci/process_files.py
```
before building the Jupyterbook.
This pre-processing script puts videos/slides into ipywidgets so they don't overlap, and links hidden cells.
Doing so is not recommended, as this will introduce changes to all notebooks in the repository that should not be committed to version control.

### Jupyter notebooks and version control

Any edits to Jupyter notebooks tend to cause significant changes to the `.ipynb` files that contain them.
Committing these changes as it pollutes the edit history.
When used with version control, such as `git`, this makes - if not to impossible - to see what has been changed, and increases the size of the diffs.

One minimal approach to avoid this is to clear the outputs to all cells ("Edit -> Clear Outputs of All Cells" in Jupyterlab) every time you safe the notebook.
Removing the outputs is not an issue, as Jupyterbook re-executes all the notebooks before turning them into HTML files.

Having to remove all outputs before each saving of each notebook is cumbersome and error-prone.
An easier way to achieve this is to install [nbstripout](https://github.com/kynan/nbstripout) and have it run automatically whenever committing notebook changes to the (local) git repository.
To install `nbstripout` for use in the repository, navigate to your local copy and call (again assuming the use of uv)
```Shell
uv pip install nbstripout
```
Then install `nbstripout` as a git filter to your local repository using
```Shell
uv run nbstripout --install
```
You can check its installation by
```Shell
uv run nbstripout --status
```
and by inspecting its installation in `.git/config`.

Once installed, all cell outputs are cleared whenever 

### Some style recommendations

#### Videos and notes

All videos are hosted on YouTube (thanks, Ella!), and should be included in Jupyter notebooks using
```Python
# @markdown 
from IPython.display import YouTubeVideo
video = YouTubeVideo(id="[YouTube ID]", width=730, height=410, fs=1)
print("Video available at https://youtube.com/watch?v=" + video.id)
video
```
where `[YouTube ID]` is replaced with the respective YouTube video id (e.g., `YBCLN8NnrjM` for Video 1.1).

All notes are hosted in their own [OSF.io project](https://osf.io/t95wk/) (thanks, Ella!). Links to individual notes should be included first as a download link in a markdown cell, using
```Markdown
<a href="https://osf.io/[OSF id]/download">Click here to download notes</a>
```
where `[OSF id]` is the respective note's OSF id (found by choosing the respective file in the OSF.io project).
Second, the note should be displayed in an iframe with the following Python code
```Python
# @markdown
from IPython.display import IFrame
IFrame(src="[OSF IFrame url]", width=730, height=1000)
```
where the `[OSF IFrame url]` is found by choosing the `Export -> Copy static HTML iFrame` (top right in 'Details' tab) on the file's page on OSF.io.
