# Mathematical Tools for Neuroscience (Neurobio 212 at Harvard)

*Initially developed and taught by Ella Batty, Lucy Lai, Alex Chen, and John Assad, updated by Kanaka Rajan, Jan Drugowitsch, Gabriel Kreiman, and Caleb Weinreb.*

Course contacts: kanaka_rajan@hms.harvard.edu, jan_drugowitsch@hms.harvard.edu, gabriel.kreiman@tch.harvard.edu, calebsw@gmail.com

The course material is available as a [jupyterbook](https://rajanlab.github.io/MathTools2026/) hosted as a Github page. The source files used to build this jupyterbook are available in this repository. Please see below for instructions on how to build the course webpage locally.

### Description of course

Numerical data analysis has become a nearly indispensable tool in modern neuroscience. This course aims to equip graduate students with the fundamental mathematical skills in quantitative modeling and data analysis necessary for neuroscience research (and for further computational neuroscience courses). **This course is essentially organized into three sections: one on linear algebra, one on probabiliy & statistics, and one on the basics of machine learning.**
 We will also cover some additional topics such as differential equations and dynamical systems). 

One goal in formulating this course was to alleviate the need for taking multiple undergraduate-level courses in each of the stated topics (which may be cumbersome due to back-and-forth commute, inconvenient scheduling, or just an excess of materical with no clear applicability to neuroscience research).  Our goal is to make this as fun, approachable, and applicable as possible. We would like to build mathematical intuition for these essential topics.  

### Course Prerequisites

You will not need any math experience beyond high school calculus. Python will be used in this class so some knowledge of it is necessary, although this course will also serve as an opportunity to practice those skills.  

### Description of materials

There are three components to the course: video lectures, comprehension questions, and tutorials.

**Video lectures**: The course consists of short video lectures each structured around a specific topic (10-20 minutes per video). We have created most of these videos using a Khan academy inspired style. We don't want to reinvent the wheel so when great videos already exist on a specific topic, we link to those instead, but this will mostly occur in the linear algebra section. 

**Comprehension questions**: These are short questions designed to be looked at right after watching the videos to consolidate your knowledge and try out quick computations. These questions are administered through the course page on Canvas and are not available in this repository.

**Tutorials**: Each week has 1 - 2 tutorials, or problem sets. These are Jupyter notebooks with exercises where you might be asked to do computations by hand, engage with interactive demos, or code. They are designed to review the video material and in some cases introduce new concepts. They are not designed for repetitive problem solving (i.e. you will not be asked to solve a matrix equation by hand 100 times...). 

### Other resources

Helpful for before this course: [Basic Introduction to Maths and Python for Neuroscience by John Butler](https://github.com/john-s-butler-dit/Basic-Introduction-to-Python)

Similar course: [Mathematical Tools for Neural and Cognitive Science by Eero Simoncelli & Mike Landy](https://www.cns.nyu.edu/~eero/math-tools/)

A good follow-up to learn computational neuroscience: [Neuromatch Academy](https://github.com/NeuromatchAcademy/course-content)

### Building the course webpage locally

To create a local copy of the course webpage (e.g., to change its content), clone the repository and build the jupyterbook locally. The latter is achieved by first installing the required packages into a virtual environment (here assuming the use of the uv package manager):
```Shell
uv venv --python 3.13
uv pip install -r requirements.txt
```
Once installed, the jupyterbook is built by calling
```
uv run jupyter-book biild .
```
Once completed, the course webpage will be available at `_build/html/index.html`.

Note that this will _not_ produce an exact copy of the course webpage, as it does not pre-process the jupyter notebooks. This is done to avoid modifying each of these files, which makes version control tricky. In order to perform this pre-processing if desired, additionally run
```
uv run ci/process_files.py
```
before builing the jupyterbook. This pre-processing script puts videos/slides into ipywidgets so they don't overlap, and links hidden cells.
