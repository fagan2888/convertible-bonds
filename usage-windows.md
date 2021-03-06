USING THE WINDOWS BINARY
========================

Using ecb directly
------------------

You can use `ecb` directly. The windows binary is `ecb.exe` in the directory `ecb`. This is the only file that you need if you plan to use `ecb` directly under Windows. All other files in this distribution are then redundant. But you may still find `ecb-run-raw.bat` useful.

`ecb` takes only one argument which is the input file. If this argument is omitted `ecb` reads input from standard input so that you can pipe input into `ecb` from some other program.

`ecb` takes `XML` input and produces `XML` output. It is designed to be used in conjunction with some `XML` tools that will do error checking on the input file and format the output for human reading. This is discussed below.


Using ecb with `XML` tools
------------------------

Since `ecb` reads `XML` inputs and produces `XML` output, I strongly recommend that you use `ecb` in conjunction with some `XML` tools.

1. `ecb` does no error checking on the input. The way I use `ecb` is to pass the input file through an `XML` Schema Validator which does the error checking by ensuring that the input file corresponds to the schema defined in `ecbdata.xsd`.

    `XML` Schema Validators are available for free download.  I use `xsv` from the W3 Consortium ([here](http://www.w3.org/XML/Schema) or [here](http://www.ltg.ed.ac.uk/software/xml/) or [here](ftp://ftp.cogsci.ed.ac.uk/pub/XSV/XSV12.EXE))

2. The `XML` output is not designed for human reading, but is ideal if you want to use that output as an input to another program. The way I use `ecb` is that I pass its output through an `XSLT` processor using the `XSL` file `xmlout.xsl`. If you do not like the output format you can design your own `XSL` file.

   `XSLT` processors are also available for free download.  I use `sabcmd` from the [Ginger Alliance](http://www.gingerall.com)

Batch files for combining `ecb` with `XML` tools
--------------------------------------------

Included in the distribution are three batch files that combine `ecb` with `XML` tools in different ways.

1. `ecb-run-raw.bat` uses no `XML` tools. It simply runs `ecb` and pipes the output through `more` for easier reading. Alternatively, it can send output to a file.  Usage `ecb-run-raw [--help] infile [outfile]`

2. `ecb-run-nocheck.bat` passes the output through an `XSLT` processor to produce human readable output. This output is piped through `more` or sent to an output file.  Usage `ecb-run-nocheck [--help] infile [outfile]` To use this, you must download and install an `XSLT` processor and change the line `set xslate=sabcmd` to set the correct path and program name of the `XSL` Processor.

3. `ecb-run.bat` passes the input file through an `XML` Schema Validator which ensures that the file conforms to the schema definition. Only then does it run `ecb`. The output is passed through an `XSLT` processor to produce human readable output. This output is piped thorugh "more" or sent to an output file.  Usage `ecb-run [--help] infile [outfile]` To use this, you must download and install an `XSLT` processor and change the line `set xslate=sabcmd` to set the correct path and program name of the `XSL` Processor.  In addition, you must download and install an `XML` Schema Validator and change the line `set validate="C:\Program Files\xsv\xsv"` to set the correct path and program name of the `XML` Schema Validator.


BUILDING `ECB` 
============
              
`ecb` can be built under Linux (or a Linux-like environment under Windows) using `gcc`. The Windows binary was built using gcc 2.95 under Cygwin in Windows 98. It was built to link with the MINGW library to produce a binary that runs as a native Windows application without any other dll's.

I believe that `ecb` does not use any Unix specific or Windows-specific features and should build smoothly in any Operating System. It compiles with the -pedantic switch set in `gcc` implying that it conforms strictly to ANSI C++ and does not use any gcc-specific features. It should therefore compile with any other C++ compiler that conforms to ANSI C++. It does however need a modern C++ compiler as it uses C++ templates and namespaces extensively. It also uses the Standard Template Library (STL).

I would imagine that if you have a modern C++ compiler, you should be able to build `ecb` in any environment without difficulty.

If you are in a Unix clone that supports make, you can use the Makefile in the source directory under `ecb`. Just `cd` to this directory and run `make` to build `ecb` and run `make clean` to remove all the unwanted object files.  The Windows binary in this distribution was created using `make MINGW=1` to compile in the MINGW libraries while running `gcc` under `cygwin`.  But I see no reason to use this switch except to produce a Windows binary for distribution.

If you want to build under MS Visual C++ or some other development environment which does not support make, you need to compile all the .cpp files listed in the makefile and link all of them together. Of course, you need a modern compiler that supports templates, namespaces and STL.

COPYRIGHT
---------

The program `ecb` is copyrighted and distributed under GNU GPL. Copyright (C) 2001 Prof. Jayanth R. Varma, jrvarma@iima.ac.in, Indian Institute of Management, Ahmedabad 380 015, INDIA

The program ecb uses the software `AdvXMLParser` Copyright 1999,2000 Sebastien Andrivet which is covered by a separate license (see the `License` file in the `AdvXMLParser` folder)
