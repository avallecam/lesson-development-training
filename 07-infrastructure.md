---
title: The Carpentries Workbench
teaching: 45
exercises: 20
---

::::::::::::::::::::::::::::::::::::::: objectives

- Identify the key tools used in The Carpentries lesson infrastructure.
- Complete the fundamental setup steps for a new lesson repository.
- Edit Markdown files using the GitHub web interface.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How is a lesson site set up and published with GitHub?
- What are the essential configuration steps for a new lesson?
- How do you create and modify the pages in a lesson?

::::::::::::::::::::::::::::::::::::::::::::::::::

At this stage in the training, 
you should have a clear idea of who the people are that you want to teach this lesson to,
and what exactly the skills are that you want them to learn while they are following it.
It is time to begin creating a website that will present that lesson to the world!

## GitHub Pages

The source of all The Carpentries lessons is made publicly-available in repositories on [GitHub].
By making our repositories public like this,
we encourage others to help us maintain and improve our lessons,
and make it as easy as possible for them to re-use and modify our lessons for their own purposes.

GitHub provides a hosting service to open source projects such as these,
allowing users to present their projects to the wider world.
The repository includes a complete history of the changes made 
between versions of the individual files in the project,
and provides many features that facilitate collaboration on projects.
We will learn more about some of those collaborative features later in this training.
For now, we will focus on one other important feature that GitHub provides: website hosting.

Via a system called **GitHub Pages**, users can build and host websites 
from the files present in any repository on GitHub.
For many years, 
this has been how The Carpentries presents its lesson websites to the world.

## Using The Carpentries Workbench

Carpentries lesson websites are built with [**The Carpentries Workbench**][workbench],
a toolkit that converts Markdown and RMarkdown files into the HTML
that can be served by GitHub Pages.
We will use it now to initialise a new lesson.

::: callout

### A Brief History of The Carpentries Lesson Infrastructure

In the past, our lesson sites were generated by software called _[Jekyll]_, 
a tool built into GitHub Pages that allows the webpage content, 
written in the text files of the repository, 
to be combined with descriptions of settings, 
structure,
and styling,
to create a website.
The template used by Jekyll to structure and style lessons 
was initially developed in 2013/2014
by Abby Cabunoc Mayes, Greg Wilson, Jon Pipitone, and Michael Hansen
for [Software Carpentry][swc-home].
It was [expanded and maintained by many members of the community][styles-contributors]
over almost a decade,
to also support [Data Carpentry][dc-home], [Library Carpentry][lc-home], and many other lessons.

In 2022, we adopted a new infrastructure for our lesson sites: **The Carpentries Workbench**.
Lesson sites built on the Workbench are still hosted with GitHub Pages,
but no longer use Jekyll.
Instead, the lessons are built using [a programming language, _R_][R], and _[pandoc]_, 
a software designed for converting content between file formats.
The Workbench combines three R packages:

- `{sandpaper}`: 
   converts a collection of Markdown or RMarkdown files into
   the structure of a lesson website.
- `{varnish}`: provides the files and folders that add 
   styling and additional functionality to a lesson website.
- `{pegboard}`: an programmatic interface to the lesson, 
   enabling various automated validation tasks.

For lesson developers, 
the Workbench makes The Carpentries lesson repositories
much simpler to navigate and work with.

:::

### Creating a Lesson Repository

To get started, we first need to create a new repository for our lesson.
We will use a template to do this, 
so that the new repository contains the basic files and folders
that the Workbench needs in order to build a lesson site.
There are currently two templates to choose between:

1. [A Markdown template][md-template]
2. [An RMarkdown template][rmd-template], best suited to lessons that will include R source code that will generate output.

**One member of each participating lesson team** should choose one of these templates, 
following the link above and completing the configuration as follows:

* add a name for the repository
  * The name should be descriptive but fairly brief,
    with hyphens (`-`) to separate words
  * the name can always be changed later, via the repository settings
* in the "Description" field, write the title of your lesson
* choose "Public" visibility
* make sure the "Include all branches" box is checked

After pressing the _Create repository using this template_ button,
you should be presented with a brand new lesson repository.

TODO insert screenshot of repository structure here

#### Adding collaborators

To be able to add content to the lesson,
your collaborators on this project will need access to the repository.
To add collaborators to the repository, 
navigate to _Settings_, then choose _Collaborators_ from the left sidebar.
Now repeat the following steps for every collaborator working with us on the project.

- Click _Add people_ and enter the GitHub username of one of our collaborators.
- Click _Add USERNAME to this repository_.

Your collaborator should receive an email inviting them to join the repository. 
After they have accepted this invitation, they should be able to edit the repository,
adding new files and modifying existing ones. 
Only the person who created the repository will be able to adjust the repository settings.

### Repository Files

The repository contains a number of files and folders.
Most of these are source files for the content of our new lesson,
but a few are accompanying files primarily intended for the repository itself
rather than the lesson website.
These are:

- `CODE_OF_CONDUCT.md`
- `CONTRIBUTING.md`
- `LICENSE.md`
- `README.md`
- `.gitignore`
- and the `.github/` folder.

We will address all of the files later in the training.
For now, we will move on to complete the basic setup of the lesson.

### Configuring a Lesson Repository

#### Activating GitHub Pages

We need to tell GitHub to begin serving the lesson website via GitHub Pages.
To do this, navigate to _Settings_, then choose _Pages_ from the left sidebar.
Under _Source_, choose the `gh-pages` branch, leave the folder set to `/ (root)`,
and click _Save_.
Now, copy the URL in the box: this will be the address of your lesson site.

::: callout

### Which branch to use?

Although we configure GitHub Pages to serve the lesson website from the `gh-pages` branch,
**the default working branch for a lesson will be `main`**.
For the rest of this training, you should add and edit files on `main`,
and in future, when you open Pull Requests to update the lesson content,
these should also be made to `main`.
The `gh-pages` branch should never be modified by anyone other than the automated actions-user account.

:::

Returning to the repository home page 
(e.g. by clicking the name of the project near the top left of the window),
click the gear wheel icon near the top right, to edit the _About_ box.
Paste the Pages URL into the _Website_ box and click _Save changes_.

After following these steps, when you navigate to the pages URL, you should be see a lesson website with The Carpentries logo and "Lesson Title" in the top-left corner.
You may need to wait a few minutes for the website to be generated.

#### `config.yaml`

The lesson title can be adjusted by modifying the `config.yaml` file in the repository.
The `config.yaml` file contains several global parameters for a lesson -
to determine some of the page styling, contact details for the lesson, etc -
and is written in _[YAML]_, a structured file format of key-pair values.
As well as the title of the lesson,
you can and should adjust some of the other values in `config.yaml`,
but you should not need to add new values or learn a lot about YAML 
to be able to configure your lesson.

::: challenge

### Practice with `config.yaml` (5 minutes)

Complete the configuration of your lesson by adjusting the following fields in `config.yaml`:

- `email`: add an email address people can contact with questions about the lesson/project.
- `created`: the date the lesson was created (today's date) in YYYY-MM-DD format.
- `keywords`: a (short) list of keywords for the lesson, 
   which can help people find your lesson when searching for resources online.
- `source`: change this to the URL for your lesson repository.

We will revisit the `life_cycle` and `carpentry` fields in `config.yaml` later in this training.

:::

::: challenge

### Improving the `README.md` (5 minutes)

The `README.md` file is the "front page" of your lesson repository on GitHub,
and is written in Markdown.
You should use it to provide basic information about the project,
for anyone who finds their way to the source files for your lesson.
Take a few minutes to update it with some basic information about the project:

- the lesson title
- a short description of the lesson
- a list of the names of the authors, optionally linked to their GitHub profile

:::


## Adding Lesson Content

Now that we have completed the basic configuration of a lesson site,
it is time to move on and look at where the actual lesson content will be written.

#### Lesson Home Page

The "home page" of a lesson is created from the `index.md` file:
this file should contain a brief introduction to the lesson, 
designed to give visitors to the page a first impression of the lesson
and whether it is appropriate for them.
The file begins with a short header, 
written in the same key-value pair syntax we encountered in `config.yaml`.

```markdown
---
site: sandpaper::sandpaper_site
---

```

This header configures how the site will be built by `sandpaper`,
one of the components of The Carpentries Workbench,
and should be left untouched.
The page content begins after the blank line that follows this header.

To get started on this home page,
replace the template text with 
the same title and short description you added to your `README.md`.

Below those, you can add the prerequisite skills you determined earlier for your lesson,
as a bullet point list to `index.md`:

```markdown
- prerequisite 1
- prerequisite 2
- ...
```

::::::::::::::::::::::::::::::::::::::  challenge

## Exercise: practice editing Markdown in GitHub (optional)

Add the objectives you defined for your lesson
as a bullet list in the `index.md` file of your lesson repository.


::::::::::::::::::::::::::::::::::::::::::::::::::

The main body of the lesson is written in _episodes_: 
the individual chunks or sections that the lesson is separated into.
The episode pages of the lesson site will be constructed from Markdown files
in the `episodes` folder of the lesson repository.

::: callout

### Why episodes?

TODO: add context and explanation for our use of "episodes" to describe chunks of a lesson.

:::

The `episodes` folder of the new repository contains a single file,
`01-introduction.md`. 
The content of this file includes examples of how to write Markdown files
for The Carpentries Workbench.

There are two important things to note:

1. Like `index.md`, the episode file begins with a short header.
   The fields in this header describe the episode title and the estimated time (in minutes)
   required to teach it and complete the exercises.
2. The example content includes several lines that start with strings of colons (`:::::::`).
   These mark the beginnings and ends of structural elements within the page, 
   called _fenced divs_. 
   Each fenced div starts and ends with a string of colons. 
   A word at the end of the starting colons indicates what kind of block it is. 
   We will explore them in more detail later in the training.

Let's create a new episode file, for one of the episodes you have just identified.
First, open the "raw" view of the `01-introduction.md` example episode,
and copy the first 19 lines, 
down to the blank line under the closing string of the `objectives` div.

```markdown
---
title: "Using Markdown"
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- How do you write a lesson using Markdown and `{sandpaper}`?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain how to use markdown with The Carpentries Workbench
- Demonstrate how to include pieces of code, figures, and nested challenge blocks

::::::::::::::::::::::::::::::::::::::::::::::::
```

::: instructor

Be careful here to ensure that participants who are collaborating on the same repository
do not create conflicts e.g. by editing the same file or creating files with identical names.

:::


Now create a new file in the `episodes` folder and,
based on the episodes you planned out in _Defining lesson objectives_,
choose a name for it that concisely describes the intended content.
To control the order of episodes in the lesson,
the name should start with two digits, 
e.g. `02-data-visualisation.md`.

For page content, paste those first 19 lines of the `01-introduction.md` file and:

1. replace the title
2. set the `teaching` and `exercises` fields to zero for now
3. replace the contents of the `questions` and `objectives` divs with "TODO"


```markdown
---
title: "Episode Title"
teaching: 0
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions 

- TODO

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- TODO

::::::::::::::::::::::::::::::::::::::::::::::::
```

::::::::::::::::::::::::::::::::::::::  challenge

## Exercise: practice creating episodes (10 minutes)

Repeat the steps you just saw, to create another new episode file.
If you know what another episode in your lesson will be about,
create the page for that.
Otherwise, feel free to use any values you like for the file name and episode title.

::::::::::::::::::::::::::::::::::::::::::::::::::


When these episode files have been created,
you can navigate back to the lesson website.
Refresh the page and,
under _Chapters_ in the left sidebar,
you should find the titles of all the episodes in
the `episodes` folder of your repository.
Clicking on one of those titles will take you to the episode page built from the file you created.
At the top of the page body, you will find the episode title 
and an _Overview_ box containing a list of the questions and objectives
defined for the episode.
Later, we will add more content to your chosen episodes.

TODO add a labelled screenshot of a new episode page

Using this approach, we can build up our lesson one episode at a time.

We have now learned everything we need to be able to use The Carpentries Workbench,
and our focus can return to the process of developing a new lesson.

:::::::::::::::::::::::::::::::::::::::: keypoints

- Lesson sites are built from source repositories with GitHub Pages.
- A new lesson repository can be created from a template maintained by The Carpentries, and configured by adjusting the `config.yaml` file.
- The main pages of a lesson website are created from Markdown or RMarkdown files in the `episodes` folder. 

::::::::::::::::::::::::::::::::::::::::::::::::::


[dc-home]: https://datacarpentry.org/
[GitHub]: https://github.com/
[Jekyll]: https://jekyllrb.com/
[lc-home]: https://librarycarpentry.org/
[md-template]: https://github.com/carpentries/workbench-template-md/generate
[pandoc]: https://pandoc.org/
[R]: https://www.r-project.org/
[rmd-template]: https://github.com/carpentries/workbench-template-rmd/generate
[styles-contributors]: https://github.com/carpentries/styles/graphs/contributors
[swc-home]: https://software-carpentry.org/
[YAML]: https://yaml.org/
