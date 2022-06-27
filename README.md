# QCR Shared Tools

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

Done. QCR tools can now be used by simply running `qcr ...` from any location. A temporary copy of all the tools is stored in `/var/tmp/qcr` to support offline access.

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

## Usage

The `qcr` script will run the latest version of any tool in [this directory](https://github.com/qcr/tools/tree/master/tools) via the following syntax:

```
qcr TOOL_NAME TOOL_ARG1 TOOL_ARG2 ...
```

For example, the following will run the tool for making QR-QCR tags linked to a target page:

```
qcr robot_tag "Your title" "your.email@qut.edu.au" "https://your/target/page"
```

Or to start a new ROS project using one of [our code templates](https://github.com/qcr/code_templates):

```
qcr template ros_package
```

### Adding Your Own Tools

To add a new tool:

1. Clone this repository to your computer and make sure you are on the `master` branch
2. Add the new bash tool script to the `./tools/` directory of this repository
3. Make sure your script is well documented, at the very least include a description/example on how to use it within the script itself
4. Update this ReadMe to include your tool within the list of accessible tools, along with a description and your GitHub user handle
5. Push the changes to the `master` branch.

### Reporting Tool Issues

Please use the [GitHub Issues](https://github.com/qcr/tools/issues) associated with this repository to highlight any issues with a tool or if you believe a tool's feature set should be expanded. Make sure to mention the creator of the tool using their GitHub user handle.
