# QCR Shared Tools

[![QUT Centre for Robotics Open Source](https://github.com/qcr/qcr.github.io/raw/master/misc/badge.svg)](https://qcr.github.io)
![Primary language](https://img.shields.io/github/languages/top/qcr/tools)
[![License](https://img.shields.io/github/license/qcr/tools)](./LICENSE.txt)

This repository houses the `qcr` script, which allows simple direct access to technical tools used internally at QCR. Although this repository is public (for ease of installation), we don't expect these tools to be of use outside of QCR. Contributors to this repository should be aware that the repository is public, and choose what they commit accordingly.

A list of the tools available can be found by simply running the `qcr` script. Some of the featured tools include:

- **code_template** - starts a new project using one of [our code templates](https://github.com/qcr/code_templates) (creator [btalb](https://github.com/btalb))
- **create_tag** - allows the generation of a QR-QCR tag linked to a URL (creator [btalb](https://github.com/btalb))

## Installation the tools

There are two options for installation: standalone and Git-based. Standalone, is simplest, and allows you permanent access to latest version of the tools. A Git-based installation clones the repository and allows you deeper control of subscripts and installation.

## Standalone installation

1. Pick a directory on your PATH (`~/bin/` is usually the best choice):

```
cd ~/bin/
```

2. Download the standalone script and make it executable:

```
wget -O qcr https://github.com/qcr/tools/raw/master/qcr_standalone && chmod +x qcr
```

Done. A temporary copy of all the tools will be stored in `/var/tmp/qcr` when you first run the `qcr` script to support offline access.

_Note: A `~/bin` directory can be created if it doesn't exist by running `mkdir ~/bin`. This directory is automatically sourced when you log in. You will need to log out and back in to source it for the first time after you create it. It's good practice to put any other user defined scripts that you want executable from any directory in `~/bin/`._

## Git-based installation

1. Clone the repository

```
git clone https://github.com/qcr/tools
```

2. Add the `qcr` script to somewhere on your PATH by creating a symbolic link:

```
ln -s <where_cloned_tools_repo>/qcr ~/bin/
```

## Using the script

Using the script is simple once it's on your PATH. Simply:

```
qcr --help
```

to list help information about the tool. Then

```
qcr
```

will print a list of the available tools. And finally, run a tool using:

```
qcr TOOL_NAME TOOL_ARG1 TOOL_ARG2
```

# What is actually going on

The `qcr` script runs the latest version of any tool in [the ./scripts/ directory of this repository](https://github.com/qcr/tools/tree/master/scripts). It does this by translating the following syntax:

```
qcr TOOL_NAME TOOL_ARG1 TOOL_ARG2 ...
```

Into the following command:

```
<directory_where_repo_lives>/scripts/TOOL_NAME TOOL_ARG1 TOOL_ARG2...

```

## Other special rules

That's the general principle. There a couple of special cases that help improve the tool's flexibility and usability:

- when no tool name is provided the script will either:
  - print a help menu for `qcr -h` or `qcr --help` calls
  - print the list of available commands
- when a tool name is provided the script will:
  - select the deepest tool matching the start of the arguments, for example `qcr arg1 arg2 --arg3` will look for `./scripts/arg1/arg2` then `./scripts/arg1` then throw an error if none are found
  - central commands for a tool can be specified in a file called `.command` (e.g. `./scripts/my_tool/{.command,mode_1,mode_2}` will support commands `qcr my_tool`, `qcr my_tool mode_1`, and `qcr my_tool mode_2`)
  - the matched command will receive all args after those corresponding to the matched command (e.g. `qcr my_tool mode_1 -a -b` will call `./scripts/my_tool/mode_1` with args `-a -b` or `./scripts/my_tool` with args `mode_1 -a -b` if the former doesn't exist)

## Adding Your Own Tools

To add a new tool:

1. Clone this repository, and make sure you are on the default branch
2. Add the new bash tool script to the `./scripts/` directory of this repository
3. Make sure your script is well documented, at the very least it should have a comment block at the top describing what the tool does and how to use
4. Commit and push the changes

# Reporting Tool Issues

Please use the [GitHub Issues](https://github.com/qcr/tools/issues) associated with this repository to highlight any issues with a tool or if you believe a tool's feature set should be expanded. Feel free to mention the creator of the tool, if known, using their GitHub user handle.
