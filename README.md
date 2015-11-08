# Diagcc

Diagcc is a tool that colors gcc's diagnostic message.

# Example

Make 

    $ make
    

Redirect gcc's stderr to stdout then pipe to ./diagcc (only stdout can be piped)

    $ gcc 2>&1 sample.c | ./diagcc

You will get something like this

![example](http://i.imgur.com/swTbjAG.png)

Quote from [GCC 4.9 Release Series Changes, New Features, and Fixes](https://gcc.gnu.org/gcc-4.9/changes.html)

Support for colorizing diagnostics emitted by GCC has been added. The `-fdiagnostics-color=auto` will enable it when outputting to terminals, `-fdiagnostics-color=always` unconditionally. The GCC_COLORS environment variable can be used to customize the colors or disable coloring. If GCC_COLORS variable is present in the environment, the default is `-fdiagnostics-color=auto`, otherwise `-fdiagnostics-color=never`.

Diagcc uses the same color scheme as fdiagnostics-color.

## Implementation

Diagcc is implemented with flex and bison. 

The language of the diagnostic message can be defined using by following BNF:


    text            : error_block               {;}
                    | text error_block          {;}
                    ;

    error_block     : file_name error_type messages    {color($1, $2, $3);}
                    ;

    error_type      : error_t                   {;}  /* $$ defaults to $1 */
                    | warning_t                 {;}
                    | note_t                    {;}
                    ;

    messages        : message                   {$$ = strdup($1);}
                    | messages message          {$$ = my_concate($1, $2);}
                    ;


# Install

    sh install.sh

Then restart the shell, chdir to src/ and test
    
    gcc sample.c


# Extension

Similar techque can also be used to color g++/lex/yacc's diagnostic message.

New keywords maybe added in the lexer.


