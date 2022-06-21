# QCR Shared Tools

This repository contains the `qcr` script which allows access to useful **private** tools for use by members of QCR. Please consider carefully how you use this script, who you share it with, as the tools themselves are not built for widespread use.

Tools accessible by the `qcr` script include:

- **create_tag** - allows the generation of a QR-QCR tag linked to a URL (creator [btalb](https://github.com/btalb))
- **template** - starts a new project using one of [our code templates](https://github.com/qcr/code_templates) (creator [btalb](https://github.com/btalb))

## The QCR Script

This `qcr` script is standalone and allows you to run the latest version of any of our internal QCR tools, at any time in the future.

### Installation

There is no need to clone this repo to utilise the `qcr` script. To install the script perform the following:

1. Open a terminal and cd into your user bin directory: `cd ~/bin/` - see below if you don't have this directory
2. Download the script, and make it executable: `wget https://github.com/qcr/tools/raw/master/qcr && chmod a+x qcr`

If you don't have a `~/bin/` directory simpy create it by running `mkdir ~/bin`. This directory is automatically sourced when you log in. You will however, need to log out and then log back in to source it for the first time after you created it. We recommend you put any other user defined scripts that you want executable from any directory in `~/bin/`.

### Usage

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
