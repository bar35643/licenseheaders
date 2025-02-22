# licenseheaders

[![PyPi version](https://img.shields.io/pypi/v/licenseheaders.svg)](https://pypi.python.org/pypi/licenseheaders/)
[![Python compatibility](https://img.shields.io/pypi/pyversions/licenseheaders.svg)](https://pypi.python.org/pypi/licenseheaders/)

A Python 3 tool to update, change or add license headers to all files of any of
the supported types (see below) in or below some directory.

## Usage

```
python licenseheaders.py -t gpl-v3.tmpl -o "Owner" -cy 2021 -a "Author" -d ./Dirpath -n Name -u url


usage: licenseheaders.py [-h] [-V] [-v] [-d DIR] [-f [FILES [FILES ...]]] [-b]
                         [-t TMPL] [-y YEARS] [-cy] [-o OWNER]
                         [-n PROJECTNAME] [-u PROJECTURL] [--enc ENCODING]
                         [--dry] [--safesubst] [-D] [-E [EXT [EXT ...]]]
                         [--additional-extensions ADDITIONAL_EXTENSIONS [ADDITIONAL_EXTENSIONS ...]]
                         [-x [EXCLUDE [EXCLUDE ...]]]

Python license header updater

optional arguments:
  -h, --help            show this help message and exit
  -V, --version         show program's version number and exit
  -v, --verbose         increases log verbosity (can be specified 1 to 3
                        times, default shows errors only)
  -d DIR, --dir DIR     The directory to recursively process (default: .).
  -f [FILES [FILES ...]], --files [FILES [FILES ...]]
                        The list of files to process. If not empty - will
                        disable '--dir' option
  -b                    Back up all files which get changed to a copy with
                        .bak added to the name
  -t TMPL, --tmpl TMPL  Template name or file to use.
  -y YEARS, --years YEARS
                        Year or year range to use.
  -cy, --current-year   Use today's year.
  -o OWNER, --owner OWNER
                        Name of copyright owner to use.
  -n PROJECTNAME, --projname PROJECTNAME
                        Name of project to use.
  -u PROJECTURL, --projurl PROJECTURL
                        Url of project to use.
  --enc ENCODING        Encoding of program files (default: utf-8)
  --dry                 Only show what would get done, do not change any files
  --safesubst           Do not raise error if template variables cannot be
                        substituted.
  -D, --debug           Enable debug messages (same as -v -v -v)
  -E [EXT [EXT ...]], --ext [EXT [EXT ...]]
                        If specified, restrict processing to the specified
                        extension(s) only
  --additional-extensions ADDITIONAL_EXTENSIONS [ADDITIONAL_EXTENSIONS ...]
                        Provide a comma-separated list of additional file
                        extensions as value for a specified language as key,
                        each with a leading dot and no whitespace (default:
                        None).
  -x [EXCLUDE [EXCLUDE ...]], --exclude [EXCLUDE [EXCLUDE ...]]
                        File path patterns to exclude

Known extensions: ['c:.c, .cc, .h', 'cpp:.cpp, .hpp, .cxx, .hxx, .ixx', 'csharp:.cs, .csx', 'd:.d', 'go:.go', 'groovy:.groovy', 'java:.java, .jape', 'javascript:.js, .js, .cjs, .mjs', 'kotlin:.kt, .kts, .ktm', 'objective-c:.m, .mm, .M', 'php:.php, .phtml, .php3, .php4, .php5, .php7, .phps, .php-s, .pht, .phar', 'rust:.rs', 'scala:.scala', 'swift:.swift', 'typescript:.ts, .tsx', 'script:.sh,.csh,.py,.pl', 'perl:.pl', 'python:.py', 'robot:.robot', 'xml:.xml', 'sql:.sql', 'ruby:.rb', 'vb:.vb', 'erlang:.erl,.src,.config,.schema', 'html:.html', 'css:.css,.scss,.sass', 'docker:.dockerfile', 'yaml:.yaml,.yml', 'zig:.zig']

If -t/--tmpl is specified, that header is added to (or existing header replaced for) all source files of known type
If -t/--tmpl is not specified but -y/--years is specified, all years in existing header files
  are replaced with the years specified

Examples:
  licenseheaders.py -t lgpl-v3 -y 2012-2014 -o ThisNiceCompany -n ProjectName -u http://the.projectname.com
  licenseheaders.py -y 2012-2015
  licenseheaders.py -y 2012-2015 -d /dir/where/to/start/
  licenseheaders.py -y 2012-2015 -d /dir/where/to/start/ --additional-extensions python=.j2
  licenseheaders.py -y 2012-2015 -d /dir/where/to/start/ --additional-extensions python=.j2,.tpl script=.txt
  licenseheaders.py -t .copyright.tmpl -cy
  licenseheaders.py -t .copyright.tmpl -cy -f some_file.cpp
```

If *licenseheaders* is installed as a package (from pypi for instance), one can interact with it as a command line tool:

```
python -m licenseheaders -t lgpl3 -o "Eager Hacker"
```

or directly:

```
licenseheaders -t lgpl3 -o "Eager Hacker"
```


# Installation

NOTE: this requires Python 3.5 or higher!

```
pip install licenseheaders
```

## Template names and files

This library comes with a number of predefined templates. If a template name is specified
which when matched against all predefined template names matches exactly one as a substring,
then that template is used. Otherwise the name is expected to be the path of file.

If a template does not contain any variables of the form `${varname}` it is used as is.
Otherwise the program will try to replace the variable from one of the following
sources:

- an environment variable with the same name but the prefix `LICENSE_HEADERS_` added
- the command line option that can be used to set the variable (see usage)


## Supported file types and how they are processed

*NOTE:* You can provide additional file extensions with `--additional-extensions` cli argument.
Note that file extensions which contain multiple dots, e.g. ".py.j2", are not yet supported,
use ".j2" at the moment instead.

### Languages with C style comments:
c
    extensions: .c, .cc, .h

cpp
    extensions: .cpp, .hpp, .cxx, .hxx, .ixx

csharp
    extensions: .cs, .csx

d
    extensions: .d

go
    extensions: .go

groovy
    extensions: .groovy
java
    extensions: .java, .jape

javascript
    extensions: .js, .js, .cjs, .mjs

kotlin
    extensions: .kt, .kts, .ktm

objective-c
    extensions: .m, .mm, .M

php
    extensions: .php, .phtml, .php3, .php4, .php5, .php7, .phps, .php-s, .pht, .phar

rust
    extensions: .rs

scala
    extensions: .scala

swift
    extensions: .swift

typescript
    extensions: .ts, .tsx

### Other languages

script:
- extensions .sh, .csh

perl:
- extension .pl

python:
- extension .py

xml:
- extension .xml

sql:
- extension .sql

ruby:
- extension .rb

visualbasic:
- extension .vb

erlang:
- extensions .erl, .src, .config, .schema

html:
- extensions .html

css:
- extensions .css, .scss, .sass

docker:
- extensions .dockerfile
- filenames Dockerfile

yaml:
- extensions .yaml, .yml

zig:
- extensions .zig

## pre-commit hooks

licenseheaders can be used with (pre-commit)[pre-commit]

### Using pre-commit-hooks with pre-commit

Add this to your `.pre-commit-config.yaml`

```
    - repo: https://github.com/johann-petrak/licenseheaders.git
      rev: 'master'
      hooks:
          - id: licenseheaders
            args: ["-t", ".copyright.tmpl", "-cy", "-f"]
```

## License

Licensed under the term of `MIT License`. See file [LICENSE.txt](LICENSE.txt).
