
# Table of Contents

1.  [Parsing arguments in C++](#org4c1866b)


<a id="org4c1866b"></a>

# Parsing arguments in C++

This example file is based on the [GNU argp](https://www.gnu.org/software/libc/manual/html_node/Argp-Examples.html) examples.
There are only three modifications here.

1.  Parts of the argument parsing initialization is sitting in a
    headerfile.

2.  When compiling the same `c` example for a `c++` example, `g++`
    complains:

    `error: invalid conversion from ‘void*’ to ‘arguments*’ [-fpermissive]`

    To get around that, as suggested in [this stackoverflow answer](https://stackoverflow.com/a/51775591/6474744), the following replacement was done:

        // The following commented line works in c
        // struct arguments *arguments = state->input;
        // And the line below is its cpp replacement
        struct arguments *arguments = static_cast<struct arguments *>(state->input);

3.  Another complaint during compilation rises in the line:

    `char *output_file;`

    The complaint states: `warning: deprecated conversion from string
         constant to 'char*'` The correct workaround as stated in this
    stackoverflow answer, is to replace `char *` with `char const *`.
    Hence:

        char const *output_file;
