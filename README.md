# QCR Shared Tools

[![QUT Centre for Robotics Open Source](https://github.com/qcr/qcr.github.io/raw/master/misc/badge.svg)](https://qcr.github.io)
![Primary language](https://img.shields.io/github/languages/top/qcr/tools)
[![License](https://img.shields.io/github/license/qcr/tools)](./LICENSE.txt)

![QCR tools in action](https://github.com/qcr/tools/wiki/qcr_tools.png)

This repository contains the `qcr` script, which allows simple direct access to technical tools used internally at QCR. The aim of this repository and the `qcr` is two fold:
1. For the repo to act as a place for odd tools that don't require an individual repo (e.g., the `create_tag` tool); and
2. To allow QCR users to easily gain access to present and future tools without having to dig through the QCR GitHub Organisation.

Please be aware, this repository is public for ease of installation but, we don't expect all the tools to be useful outside of QCR. Contributors to this repository should be aware that the repository is public, and choose what they commit accordingly.

A list of the tools available can be found by simply running the `qcr` script. Some of the featured tools include:

- **code-templates** - starts a new project using one of [our code templates](https://github.com/qcr/code_templates) (author [btalb](https://github.com/btalb))
- **latex-templates** - starts a new latex project using one of [our latex templates](https://github.com/qcr/latex-templates) (author [jmount1992](https://github.com/jmount1992))
- **create-tag** - allows the generation of a QR-QCR tag linked to a URL (author [btalb](https://github.com/btalb))
- **system-configs** - a series of scripts for managing and tracking system configuration settings on shared systems (author [btalb](https://github.com/btalb))
- **services** - a series of scripts for managing services and start-up service configurations (author [jmount1992](https://github.com/jmount1992))

## Installing the tools

There are two options for installation: standalone and Git-based. Standalone, is simplest, and allows you permanent access to latest version of the tools. A Git-based installation clones the repository and allows you deeper control of subscripts and installation.

## Standalone installation

1. Pick a directory on your PATH (`/usr/bin/` is recommended on shared machines, or `~/bin` on personal machines), download the standalone script and make it executable. 

For shared machines run:
```
sudo wget -O /usr/bin/qcr https://github.com/qcr/tools/raw/master/qcr_standalone && sudo chmod 775 /usr/bin/qcr
```

For personal machines run:
```
wget  -O ~/bin/qcr https://github.com/qcr/tools/raw/master/qcr_standalone && chmod 775 ~/bin/qcr
```

2. Run `qcr` to install the scripts and use the tool. 

**Notes**:
- The tool will be stored in `/var/tmp/qcr` when you first run the `qcr` script to support offline access.
- A `~/bin` directory can be created if it doesn't exist by running `mkdir ~/bin`. This directory is automatically sourced when you log in. You will need to log out and back in to source it for the first time after you create it. It's good practice to put any other user defined scripts that you want executable from any directory in `~/bin/`.

## Git-based installation

Recommended for personal machines only.

1. Clone the repository

```
git clone https://github.com/qcr/tools
```

2. Add the `qcr` script to somewhere on your PATH by creating a symbolic link:

```
ln -s <where_cloned_tools_repo>/qcr ~/bin/
```

## Using the script

Using the script is simple once it's on your PATH. Any tool can be run via:

```
qcr TOOL_NAME TOOL_ARG1 TOOL_ARG2
```

Help information is also available for the main script:

```
qcr --help
```

And all tools:

```
qcr TOOL_NAME --help
```

A list of available tools can also be seen by simply invoking the tool with no arguments:

```
qcr
```

# What is actually going on

The `qcr` script calls the latest version of the desired tool in the [./scripts/](/scripts/) directory of this repository. It does this by translating the following syntax:

```
qcr TOOL_NAME TOOL_ARG1 TOOL_ARG2 ...
```

Into the following command:

```
<directory_where_repo_lives>/scripts/TOOL_NAME TOOL_ARG1 TOOL_ARG2...

```

For standalone tools (i.e., ones without a separate repo, for example the [create_tag](/scripts/create_tag) tool), the tool will be invoked as is with the passed arguments. For separate tools (i.e., ones with a separate repo, for example the [services tool](https://github.com/qcr/services)), the scripts contained in the [./scripts/](/scripts/) directory of this repository: install the tool; check for the latest version; and then invoke the individual tool with the passed arguments.

## Other special rules

That's the general principle. There a couple of special cases that help improve the tool's flexibility and usability:

- when no tool name is provided the script will print the list of available commands.
- when a tool name is provided the script will go through the following process:
  1. select the deepest tool matching the start of the arguments, for example `qcr arg1 arg2 --arg3` will look for `./scripts/arg1/arg2` then `./scripts/arg1` then throw an error if none are found
  2. check if a central command has been requested in a file called `.command` (e.g. `./scripts/my_tool/{.command,mode_1,mode_2}` will support commands `qcr my_tool`, `qcr my_tool mode_1`, and `qcr my_tool mode_2`)
  3. pass all remaining args to the matched command (e.g. `qcr my_tool mode_1 -a -b` will call `./scripts/my_tool/mode_1` with args `-a -b` or `./scripts/my_tool` with args `mode_1 -a -b` if the former doesn't exist)

## Adding Your Own Tools

To add a new tool:

1. Clone this repository, and make sure you are on the default branch
2. Add the new bash tool script to the `./scripts/` directory of this repository.
  - There is a [`template`](/scripts/template) for tools stored in separate repositories.
  - Ensure the bash script is executable, run: `chmod 775 <script>` 
3. Make sure your tool is well documented, at the very least it should have a comment block at the top describing what the tool does and how to use
4. Commit and push the changes

For an example of a standalone tool see the [create_tag](/scripts/create-tag) tool. For an example of a tool stored in a separate repository see the [Services](https://github.com/qcr/services) tool.

**Note**: while developing your own tool you may wish to use the `--tool-dir` and `--force-update-check` arguments; run `qcr --help` for more information.

# Reporting Tool Issues

Please use the [GitHub Issues](https://github.com/qcr/tools/issues) associated with this repository to highlight any issues with a tool or if you believe a tool's feature set should be expanded. Feel free to mention the creator of the tool, if known, using their GitHub user handle.
