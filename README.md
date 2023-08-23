# Project Template
Research projects are complicated. They often last for months (to years) and involve a wide range of approaches, including experiments, analyses, and communicating. Organizing this amount of information in an accessible way is critical for ensuring the project stays on track. Research projects are also community affairs; multiple people often interact and share ideas over the same project. I've been thinking about different ways to organize and manage reserach projects, and thought that a GitHub repository could provide an excellent environment for this. This is for two main reasons. 

First, GitHub repositories are ideal for maintaining all of the data, code, results, thoughts, and writing associated with a research project. The goal of this template is to facilitate using GitHub in this fashion - it is intended to be a helpful scaffold for organizing your project. GitHub automatically keeps track of changes. And it can easily be shared for collaboration.

Second, we can use the 'Issues' tracker to keep track of progress and ideas. When we have a new analysis idea or question, we simply create an Issue. As we tackled the issue (e.g., doing a suggested analysis), we can reply to the issue (including figures, text, and links to the associated scripts, etc.). When done, we can mark an issue as completed. In this way, we have a permanent record of our analysis ideas, our results, and our discussions. Even if we move on from an analysis, it stays tracked for us to revisit in the future as needed! You can even write equations using Latex; just surround text with `$` (inline) or `$$` (paragraph), such as $x_t=-x_{t-1}+I_t$ .

This template was heavily influence by a [post from Ryan Abernathy on Medium](https://rabernat.medium.com/scientific-collaboration-and-project-management-in-github-d74f2255ae5f) and the therein referenced [GitHub template](https://github.com/jbusecke/cookiecutter-science-project).

### Using the template
To use the template, simply create a new repository with your `project_name` in GitHub and use this as the starting template. The repository can either be part of the buschmanlab GitHub account or on your personal GitHub account. Either way, _it is suggested that you keep the project repository marked as private_.

### Tracking ideas and to-dos
The nice thing about Github is that we can use the built-in issue tracking to keep track of progress. Of course, this could include issues with the code itself (i.e., bugs). But, more importantly, we can keep track of a wish list of _features_ where the features of a scientific project is the analyses. This allows us to use issues to track all of our ideas for analyses, creating sub-issues for tracking progress on the code, and even replying to the issues with the figures that we generate!

### Version control with git
One of the nice things about using GitHub to manage the project, is that everything is automatically backed up with version control. This should be integrated into your analysis pipeline, whether using Python or Matlab. Please _update your repository regularly_. I would suggest doing this at least daily. This not only provides a log of your progress, but will also allow you to roll back to previous versions easily. It also allows you to easily respond to issues, knock off to-do lists, etc. 

Updates can be done automatically (e.g., [here is one solution on Windows](https://gist.github.com/rosharp/c195e67318362ed603148058875327e0)). 

### Sharing with GitHub
Need to share your results with someone? Simply add them as a collaborator on the project! They'll be able to see all of your analyses and results, read background information on the project, understand the methods you have used, and even add their own voice to the project. This is the beauty of working with GitHub; everything is online and easily shared.

Furthermore, once it is time to publish your manuscript, it is easy to create a publically accessible branch of the repository for reviewers and readers to browse.

## General Principals
This is intended to be a helpful scaffold for organizing your thoughts, analyses, results, and writing related to a project. Some suggestions for how to organize the project:

- __Avoid repetitions__: When things are repeated they often can cause silent errors where one copy of something changes and the others don't. Therefore, any code that is going to be reused should be placed into a `source` code and then called from the notebooks. Similarly, data should be loaded from the data directories within each script (e.g., `xr.open_dataset('../data/raw/dataset.dat')`.
- __Document as you go__: You will rarely do it afterwards, and if that happens it will be a pain! When developing a function, it is usually good practice to start with a sketch of the function, written as comments. Then, as you code make sure to explain any code that isn't going to be completely obvious. Finally, it is always helpful to add a description at the top along with descriptions of inputs and outputs.
- __Create unit tests__: When you develop a function, it is important to test it with known inputs/outputs (e.g., using simulated data). It is good coding practice to turn the snippets of code you wrote to test the function into a [unit test](https://en.wikipedia.org/wiki/Unit_testing). Tests are a great way of ensuring functions always return the expected output and documenting what a function is supposed to do.
- __Use notebooks to organize results__: Once you have results, you will want to organize them and make them easy to peruse in the future. Notebooks are useful for this process. You can create a notebook that presents results with code ([example](https://github.com/jbusecke/guides/blob/master/analysis_sharing_workflow.md)). This keeps everything in one place and avoids the need to write up the same passages in an email with a bunch of loose figures.
  
If you have suggestions, feel free to raise an issue or submit a pull request for this template!

## Organization

To help you organize your project, this template creates a folder structure for each part of the project. 
Your `project_name` folder should look like this:

```
├── setup.py
├── README.md             <- The top-level README for the project. Should describe the project goals and
|                            provide an overview of the contents.
├── STYLING.md            <- Maintaining a consistent style across the project is important. This document will include details about
|                            the color scheme and style of the analysis (e.g, selecting a specific color for a brain region).
├── LICENSE
│
│
├── background            <- Relevant papers and reviews. Summaries of the manuscripts and the findings.
|
├── data                  <- All data should be clearly described. There are three different types of data, each stored in a separate
|   |                        directory, as described below. It is not recommended to keep the data in the repository, rather
|   |                        the folders should include:
|   |                            1) a description of where to find the data (including link)
|   |                            2) a script for downloading the data from another source (e.g., cup)
│   ├── raw               <- Immutable raw data. This likely includes behavioral data as well as neural data. This should never
|   |                        be edited directly.
│   ├── processed         <- Datasets that were processed from `raw` folder. This is usually the data that will be analyzed.
│   └── interim           <- Small subset datasets that are used for steps along the analysis pipeline or to hold results in
|                            analyses (e.g., from notebooks).
│
├── methods               <- Catalog of the methods used to collect the data. This could include data dictionaries, manuals,
|                            and all other explanatory materials needed to understand how the data was collected. In short, this
|                            should be the basis for the methods section of the publication and so it will likely include details
|                            on the behavioral task, the method of data collection, etc.
│
├── notebooks             <- Analysis notebooks. Define and maintain a naming convention. It is recommended to include some
|                            form of version number and author in the filenames. e.g. `1.0-tjb-initial-data-exploration`. The
|                            naming convention should be clearly described in the `README.md` file.
│
├── source                <- Source code for analyses. These should be organized according to your project needs, but it is
|   |                        strongly suggested that you include scripts for loading the data from the `raw` folder and for
|   |                        creating the `processed` data files. Essentially, any time you use a function more than once it
|   |                        should _not_ be in a notebook but incorporated into a source file.
│   └── tests               <- Directory that contains tests for all of the source files. 
│
├── manuscript            <- Manuscript documents. If working locally, then should include all files (including drafts). If working
|   |                        on the cloud (e.g., Google Docs or Overleaf), then provide a link to the file in README.md and
|   |                        include the final versions when done.  
|   └── figures           <- Folder for the figures, as well as the data and scripts needed to generate the figures. All should
|                            be as compact as possible in order to facilitate sharing with others (e.g., when publishing).
│
└── presentations         <- Presentation documents. Includes files (or links) to all presentations related to the project.
                             This includes oral presentations (e.g., Powerpoint) as well as posters.
```

This structure supports a workflow that ensures the project is organized and, thus, easy to navigate. This makes it easy to quickly find figures that you've generated in the past, integrate results across analyses, etc. It will also facilitate writing at the end of the project.

Keeping all the elements of your project contained in this structure ensures that you can port the project from your laptop to a cluster or share it easily with other people.

### `background` folder
All projects are based on prior research. This folder should include all of the relevant literature. Ideally, this would be organized according to topic (e.g., in subfolders). In addition, it is highly recommended that you include a summary of each manuscript as it relates to the current project. These documents can be updated regularly as the project evolves. This is invaluable for thinking about how the current project relates to the literature and when writing the manuscript. An example markdown file is included `background\SummaryOfLiterature.md` but feel free to use a Word document or any other structure that makes sense to you.

### `data` folder
Contents of the data folder should not be committed to the github repository (*the data folder can be included to the .gitignore file - this is already done in the template*) . Ideally a script in `scripts` is used to download publicly available data into the `data/raw` folder. In climate science, some datasets (like large global climate model datasets) might not be available publicly or are simply too large to download quickly. In this case we recommend linking the files (using absolute filepaths) into the `data/raw` folders using a script(which itself should reside in `scripts`).
> No content of `data/raw` should ever be modified manually.

Often the raw data has to be subset, cleaned or preprocessed in some other way. It is recommended that you have a script that, either in `notebooks` or in `source`, that read data from `data/raw` and writes into `data/processed`. This ensures that anyone can reproduce the same results given the identical source data. It is also to a large part self-documenting.

### `methods` folder
This folder should include all of the documentation for the tools and techniques used during data collection. This will serve as a useful documentation for relevant literature. Ideally, this would be organized according to topic (e.g., in subfolders). In addition, it is highly recommended that you include a summary of each manuscript as it relates to the current project. These documents can be updated regularly as the project evolves. This is invaluable for thinking about how the current project relates to the literature and when writing the manuscript.

### `notebook` folder
Notebooks are a great tool for organizing code and plots, whether they are [jupyter notebooks](https://jupyter.org/) for Python or [Live Scripts](https://de.mathworks.com/help/matlab/matlab_prog/what-is-a-live-script-or-function.html) for Matlab. This folder should be where you keep all of your notebooks for analysis and plotting. If you don't use notebooks then just delete the folder!

One caveat is that notebooks can become unweidly. They combine code, notes, math, pictures etc in a single container. They tend to get messy quickly over time.
To keep tidy and presentable notebooks:
- _Properly name your notebooks_. Pick a format (e.g. '<running_no><author><short_description>.ipynb') and stick to it.
- _Keep code in notebooks to a minimum_. Ideally you want to have only short code cells to visualize data and refactor larger functions into the projects source code (see below)

### The `source` folder
A bunch of notebooks/scripts with thousands of line of code is not a great way to design reproducible science. Therefore, we want to store all reusable functions separately. The nice thing about this is that it means they can easily be shared with other people (you could even turn your project into an installable python package if you want!).

Now the only thing you have to do is write some [unit tests](https://docs.pytest.org/en/latest/), to check that your function behaves the way it is expected. These will help to check if changes you make in the future affect the outputs.

### `manuscript` folder
Each repository should (hopefully) lead to a single publication. Other projects may analyze the same data and lead to a different publication, but that would be a separate repository. This folder should hold all of the files for the associated manuscript, including final versions, drafts, cover letters, figures, etc.  

If you are writing a multi-project manuscript (e.g., a PhD thesis, then you can simply refer to the original repositories).

## Project Styling
It is very helpful to have a consistent style that is maintained throughout the project. This helps others quickly understand what you are plotting. It is suggested that you list the appropriate styles in a separate `STYLING.md` file. If organized well, this could be both machine and human readable, allowing you to automatically import styles for your figures and ensure any changes automatically propagate to each figure. An example [`STYLING.md`](STYLING.md) file is included in the template.

Colors should be chosen to be complementary to one another. There are many online resources for choosing a color scheme:
- [Coolors](https://coolors.co/)
- [VizPallete](https://projects.susielu.com/viz-palette)
- [ColorBrewer](https://colorbrewer2.org/)
- [ColorPicker](https://colorpicker.me/#google_vignette)

If using color ranges, please remember to avoid ranges that have highly non-linear perceptual qualities (e.g., don't use `jet` in Matlab!). Please also try to make your figures as accessible as possible. It is good practice to make sure your color palette is accessible to individuals with color blindness. This can be done through Adobe or via online [simulators](https://www.color-blindness.com/coblis-color-blindness-simulator/)
