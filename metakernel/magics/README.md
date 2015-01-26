# Line Magics

## `%cd`

%cd PATH - change current directory of session

This line magic is used to change the directory of the
notebook or console.

Note that this is not the same directory as used by
the %shell magics.

Example:
    %cd ..

## `%connect_info`

%connect_info - show connection information

This line magic will show the connection information for this
language kernel instance. This information is only necessary
if you are interested in making additional connections to the
running kernel.

Example:
    %connect_info

Paste the given JSON into a file, and connect with:

    $> ipython <app> --existing <file>

or, if you are local, you can connect with just:

    $> ipython <app> --existing %(key)s

or even just:
    $> ipython <app> --existing

if this is the most recent Jupyter session you have started.

## `%download`

%download URL [-f FILENAME] - download file from URL

This line magic will download and save a file. By
default it will use the same filename as the URL.
You can give it another name using -f.

Examples:
    %%download http://some/file/from/internet.txt -f myfile.txt
    %%download http://some/file/from/program.ss


Options:
-------
-f --filename  use the provided name as filename [default: None]

## `%edit`

%edit FILENAME - load code from filename into next cell for editing

This line magic will open the file in the next cell, and allow
you edit it.

This is a shortcut for %load, and appending a "%%file" as first line.

Example:
    %edit myprogram.ss

## `%help`

This is MetaKernel Python. It implements a Python interpreter.

## `%html`

%html CODE - display code as HTML

This line magic will send the CODE to the browser as
HTML.

Example:
    %html <u>This is underlined!</u>

## `%install_magic`

%install_magic URL - download and install magic from URL

This line magic will copy the file at the URL into your
personal magic folder.

Example:
    %install_magic http://path/to/some/magic.py

## `%javascript`

%javascript CODE - send code as JavaScript

This line magic will execute the CODE on the line as
JavaScript in the browser.

Example:
    %javascript console.log("Print in the browser console")

## `%kernel`

%kernel MODULE CLASS [-k NAME] - construct a kernel for sending code.

This line magic will contruct a kernel language so that you can
communicate.

Example:

    %kernel bash_kernel BashKernel -k bash

Use `%kx` or `%%kx` to send code to the kernel.

Also returns the kernel as output.

Options:
-------
-k --kernel_name kernel name given to use for execution [default: default]

## `%kx`

%kx CODE [-k NAME] - send the code to the kernel.

This line magic will send the CODE to the kernel
for execution.

Returns the result of the execution as output.

Example:

    %kernel ls -al

Use `%kernel MODULE CLASS [-k NAME]` to create a kernel.

Options:
-------
-k --kernel_name kernel name given to use for execution [default: None]

## `%latex`

%latex TEXT - display text as LaTeX

This line magic will display the TEXT on the line as LaTeX.

Example:
    %latex x_1 = \dfrac{a}{b}

## `%load`

%load FILENAME - load code from filename into next cell

This line magic will get the contents of a file and load it
into the next cell.

Example:
    %load myprog.py

## `%ls`

%ls PATH - list files and directories under PATH

This line magic is used to list the directory contents.

Examples:
    %ls .
    %ls ..

## `%lsmagic`

%lsmagic - list the current line and cell magics

This line magic will list all of the available cell and line
magics installed in the system and in your personal magic
folder.

Example:
    %lsmagic

## `%magic`

%magic - show installed magics

This line magic shows all of the install magics, either from
the system magic folder, or your own private magic folder.

## `%parallel`

%parallel MODULE CLASS [-k NAME] [-i [...]] - construct an interface to the cluster.

Example:

    %parallel bash_kernel BashKernel
    %parallel bash_kernel BashKernel -k bash
    %parallel bash_kernel BashKernel --i [0,2:5,9,...]

Use %px or %%px to send code to the cluster.

Options:
-------
-i --ids       the machine ids to use from the cluster [default: None]
-k --kernel_name arbitrary name given to reference kernel [default: default]

## `%plot`

%plot [options] backend - configure plotting for the session.

This line magic will configure the plot settings for this
language.

Examples:
    %plot --format=png matplotlib
    %plot -s 640,480 matplotlib

Note: not all languages may support the %plot magic.

Options:
-------
-f --format    Plot format (png, svg or jpg). [default: png]
-s --size      Pixel size of plots, "width,height"

## `%pmap`

%pmap FUNCTION [ARGS1,ARGS2,...] - ("parallel map") call a FUNCTION on args

This line magic will apply a function name to all of the
arguments given one at a time using a dynamic load balancing scheduler.

Currently, the args are provided as a Python expression (with no spaces).

You must first setup a cluster using the %parallel magic.

Examples:

    %pmap function-name-in-language range(10)
    %pmap function-name-in-language [1,2,3,4]
    %pmap run_experiment range(1,100,5)
    %pmap run_experiment ["test1","test2","test3"]
    %pmap f [(1,4,7),(2,3,5),(7,2,2)]

The function name must be a function that is available on all
nodes in the cluster. For example, you could:

    %%px
    (define myfunc
       (lambda (n)
         (+ n 1)))

to define myfunc on all machines (use %%px -e to also define
it in the running notebook or console). Then you can apply it
to a list of arguments:

    %%pmap myfunc range(100)

The load balancer will run myfunc on the next available node
in the cluster.

Note: not all languages may support running a function via this magic.

## `%px`

%px EXPRESSION - send EXPRESSION to the cluster.

Example:

    %px sys.version
    %px -k scheme (define x 42)
    %px x

Use %parallel to initialize the cluster.

Options:
-------
-e --evaluate  evaluate code in the current kernel, too. The current kernel should be of the same language as the cluster. [default: False]
-k --kernel_name kernel name given to use for execution [default: None]

## `%python`

%python CODE - evaluate code as Python

This line magic will evaluate the CODE (either expression or
statement) as Python code.

Examples:
    %python x = 42
    %python import math
    %python x + math.pi

## `%reload_magics`

%reload_magics - reload the magics from the installed files

Example:
    %reload_magics

This line magic will reload the magics installed in the
system, and in your private magic folder.

You only need to do this if you edit a magic file. It runs
automatically if you install a new magic.

## `%restart`

%restart - restart session

This line magic will restart the connection to the language
kernel.

Example:
    %restart

Note that you will lose all computed values.

## `%run`

%run FILENAME - run code in filename by kernel

This magic will take the code in FILENAME and run it. The
exact details of how the code runs are deterimined by your
language.

Example:
    %run filename.ss

Note: not all languages may support %run.

## `%shell`

%shell COMMAND - run the line as a shell command

This line command will run the COMMAND in the bash shell.

Examples:
    %shell ls -al
    %shell cd

 Note: this is a persistent connection to a shell.
 The working directory is synchronized to that of the notebook
 before and after each call.

You can also use "!" instead of "%shell".

## `%spell`

%spell NAME - execute a spell
%spell -l [all|learned|system] - list spells
%spell [-s] [-d] NAME - show or delete a spell

This line magic will execute, show, list, or delete the
named spell.

Examples:
    %spell renumber-cells

    %%spell test
    print "Ok!"

    %spell -l all

    %spell -d test

Options:
-------
-s --show      show spell [default: False]
-l --list      list spells [default: False]
-d --delete    delete a named spell [default: False]

# Cell Magics

## `%%debug`

%%debug - step through the code expression by expression

This cell magic will step through the code in the cell,
if the kernel supports debugging.

Example:
    %%debug

    (define x 1)

## `%%file`

%%file [--append|-a] FILENAME - write contents of cell to file

This cell magic will create or append the cell contents into/onto
a file.

Example:
    %%file -a log.txt
    This will append this line onto the file "log.txt"


Options:
-------
-a --append    append onto an existing file [default: False]

## `%%help`

This is MetaKernel Python. It implements a Python interpreter.

## `%%html`

%%html - display contents of cell as HTML

This cell magic will send the cell to the browser as
HTML.

Example:
    %%html

    <script src="..."></script>

    <div>Contents of div tag</div>

## `%%javascript`

%%javascript - send contents of cell as JavaScript

This cell magic will execute the contents of the cell as
JavaScript in the browser.

Example:
    %%javascript

    element.html("Hello this is <b>bold</b>!")

## `%%kx`

%%kx [-k NAME] - send the cell code to the kernel.

This cell magic will send the cell to be evaluated by
the kernel. The kernel must have been created use the
%%kernel magic.

Returns the result of the execution as output.

Example:

    %%kernel bash
    ls -al

Use `%kernel MODULE CLASS [-k NAME]` to create a kernel.

Options:
-------
-k --kernel_name kernel name given to use for execution [default: None]

## `%%latex`

%%latex - display contents of cell as LaTeX

This cell magic will display the TEXT in the cell as LaTeX.

Example:
    %%latex
    x_1 = \dfrac{a}{b}

    x_2 = a^{n - 1}

## `%%processing`

%%processing - run the cell in the language Processing

This cell magic will execute the contents of the cell as a
Processing program. This uses the Java-based Processing
language.

Example:

    %%processing
    setup() {
    }
    draw() {
    }

## `%%px`

%%px - send cell to the cluster.

Example:

    %%px
    (define x 42)

Use %parallel to initialize the cluster.

Options:
-------
-e --evaluate  evaluate code in the current kernel, too. The current kernel should be of the same language as the cluster. [default: False]
-k --kernel_name kernel name given to use for execution [default: None]

## `%%python`

%%python - evaluate contents of cell as Python

This cell magic will evaluate the cell (either expression or
statement) as Python code.

Unlike IPython's Python, this does not return the last expression.
To do that, you need to assign the last expression to the special
variable "retval".

The -e or --eval_output flag signals that the retval value expression
will be used as code for the cell to be evaluated by the host
language.

Examples:
    %%python
    x = 42

    %%python
    import math
    retval = x + math.pi

    %%python -e
    retval = "'(this is code in the kernel language)"

    %%python -e
    "'(this is code in the kernel language)"


Options:
-------
-e --eval_output Use the retval value from the Python cell as code in the kernel language. [default: False]

## `%%shell`

 %%shell - run the contents of the cell as shell commands

 This shell command will run the cell contents in the bash shell.

 Example:
     %%shell
        cd ..
        ls -al

Note: this is a persistent connection to a shell.
  The working directory is synchronized to that of the notebook
  before and after each call.

 You can also use "!!" instead of "%%shell".

## `%%show`

%%show [-o]- show cell contents or results in system pager

This cell magic will put the contents or results of the cell
into the system pager.

Examples:
    %%show
    This information will appear in the pager.

    %%show --output
    retval = 54 * 54

Options:
-------
-o --output    rather than showing the contents, show the results [default: False]

## `%%spell`

%%spell NAME - learn a new spell

This cell magic will learn the spell in the
cell. The cell contents are just commands (magics
or code in the kernel language).

Example:
    %%spell test
    print "Ok!"

    %spell test
    Ok!

## `%%time`

%%time - show time to run cell

Put this magic at the top of a cell and the amount of time
taken to execute the code will be displayed before the output.

Example:
    %%time
    [code for your language goes here!]

This just reports real time taken to execute a program. This
may fluctuate with number of users, system, load, etc.
