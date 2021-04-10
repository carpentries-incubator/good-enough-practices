---
title: "Project Organization"
teaching: 0
exercises: 0
questions:
- ""
- ""
- ""
objectives:
- ""
- ""
- ""
keypoints:
- ""
- ""
- ""
---

Organizing the files that make up a project in a logical and consistent
directory structure will help you and others keep track of them. Our
recommendations for doing this are drawn primarily from [[noble2009](#noble2009),
[gentzkow2014](#gentzkow2014)]

### Put each project in its own directory, which is named after the project.

Like deciding
when a chunk of code should be made a function, the ultimate goal of
dividing research into distinct projects is to help you and others
best understand your work. Some researchers create a separate
project for each manuscript they are working on, while others group
all research on a common theme, data set, or algorithm into a single
project.

As a rule of thumb, divide work into projects based on the overlap
in data and code files. If two research efforts share no data or
code, they will probably be easiest to manage independently. If they
share more than half of their data and code, they are probably best
managed together, while if you are building tools that are used in
several projects, the common code should probably be in a project of
its own. Projects do often require their own organizational model,
but the below are recommendations on how you can structure data,
code, analysis outputs and other files. The important concept is
that is useful to organize the project by the types of files and
that consistency helps you effectively find and use things later.

### Put text documents associated with the project in the `doc` directory.

This includes
files for manuscripts, documentation for source code, and/or an
electronic lab notebook recording your experiments. Subdirectories
may be created for these different classes of files in large
projects.

### Put raw data and metadata in a `data` directory, and files generated during cleanup and analysis in a `results` directory

where "generated
files" includes intermediate results, such as cleaned data sets or
simulated data, as well as final results such as figures and tables.

The `results` directory will *usually* require additional
subdirectories for all but the simplest projects. Intermediate files
such as cleaned data, statistical tables, and final
publication-ready figures or tables should be separated clearly by
file naming conventions or placed into different subdirectories;
those belonging to different papers or other publications should be
grouped together. Similarly, the `data` directory might require
subdirectories to organize raw data based on time, method of
collection, or other metadata most relevant to your analysis.

### Put project source code in the `src` directory.

`src` contains all of
the code written for the project. This includes programs written in
interpreted languages such as R or Python; those written compiled
languages like Fortran, C++, or Java; as well as shell scripts,
snippets of SQL used to pull information from databases; and other
code needed to regenerate the results.

This directory may contain two conceptually distinct types of files
that should be distinguished either by clear file names or by
additional subdirectories. The first type are files or groups of
files that perform the core analysis of the research, such as data
cleaning or statistical analyses. These files can be thought of as
the "scientific guts" of the project.

The second type of file in `src` is controller or driver scripts
that that contains all the analysis steps for the entire project
from start to finish, with particular parameters and data
input/output commands. A controller script for a simple project, for
example, may read a raw data table, import and apply several cleanup
and analysis functions from the other files in this directory, and
create and save a numeric result. For a small project with one main
output, a single controller script should be placed in the main
`src` directory and distinguished clearly by a name such as
"runall". The short example in Figure [fig:script] is typical of
scripts of this kind; note how it uses one variable, `TEMP_DIR`, to
avoid repeating the name of a particular directory four times.

    TEMP_DIR = ./temp_zip_files

    echo "Packaging zip files required by analysis tool..."
    mkdir $(TEMP_DIR)
    ./src/make-zip-files.py $(TEMP_DIR) *.dat

    echo "Analyzing..."
    ./bin/sqr_mean_analyze -i $(TEMP_DIR) -b "temp"

    echo "Cleaning up..."
    rm -rf $(TEMP_DIR)

### Put compiled programs in the `bin` directory

`bin` contains
executable programs compiled from code in the `src` directory[^19].
Projects that do not have any will not require `bin`.

> **Scripts vs. Programs**
>
> We use the term "script" to mean "something that is executed
> directly as-is", and "program" to mean "something that is
> explicitly compiled before being used". The distinction is more
> one of degree than kind—libraries written in Python are actually
> compiled to bytecode as they are loaded, for example—so one other
> way to think of it is "things that are edited directly" and
> "things that are not".

> **External Scripts**
>
> If `src` is for human-readable source code, and `bin` is for
> compiled binaries, where should projects put scripts that are
> executed directly—particularly ones that are brought in from
> outside the project? On the one hand, these are written in the
> same languages as the project-specific scripts in `src`; on the
> other, they are executable, like the programs in `bin`. The answer
> is that it doesn't matter, as long as each team's projects follow
> the same rule. As with many of our other recommendations,
> consistency and predictability are more important than
> hair-splitting.


### Name all files to reflect their content or function.

For example, use names
such as `bird_count_table.csv`, `manuscript.md`, or
`sightings_analysis.py`. Do *not* using sequential numbers (e.g.,
`result1.csv`, `result2.csv`) or a location in a final manuscript
(e.g., `fig_3_a.png`), since those numbers will almost certainly
change as the project evolves.

### Example

The diagram in Figure [fig:project] provides a concrete example of how a
simple project might be organized following these recommendations:

    .
    |-- CITATION
    |-- README
    |-- LICENSE
    |-- requirements.txt
    |-- data
    |   -- birds_count_table.csv
    |-- doc
    |   -- notebook.md
    |   -- manuscript.md
    |   -- changelog.txt
    |-- results
    |   -- summarized_results.csv
    |-- src
    |   -- sightings_analysis.py
    |   -- runall.py

The root directory contains a `README` file that provides an overview of
the project as a whole, a `CITATION` file that explains how to reference
it, and a `LICENSE` file that states the licensing. The `data` directory
contains a single CSV file with tabular data on bird counts
(machine-readable metadata could also be included here). The `src`
directory contains `sightings_analysis.py`, a Python file containing
functions to summarize the tabular data, and a controller script
`runall.py` that loads the data table, applies functions imported from
`sightings_analysis.py`, and saves a table of summarized results in the
`results` directory.

This project doesn't have a `bin` directory, since it does not rely on
any compiled software. The `doc` directory contains two text files
written in Markdown, one containing a running lab notebook describing
various ideas for the project and how these were implemented and the
other containing a running draft of a manuscript describing the project
findings.


> ## Attribution
> Content of this episode was adopted after Wilson et al.
> [Good Enough Practices for Scientific Computing](https://github.com/swcarpentry/good-enough-practices-in-scientific-computing).
{: .callout}

## I am a section

With a text.

> ## I am a yellow info
>
> And my text.
{: .callout}


~~~
I am code
~~~
{: .source}


> ## I am a problem
>
> Defined here.
>
>> ## Solution
>>
>> *   I am an answer.
>> *   So am I.
> {: .solution}
{: .challenge}




{% include links.md %}
