# QCR Shared Tools

This repository contains the `qcr` script which allows access to useful **private** tools for use by members of QCR. Please consider carefully how you use this script, who you share it with, as the tools themselves are not built for widespread use.

Tools accessible by the `qcr` script include:
- **create_tag** - allows the generation of a QR-QCR tag linked to a URL
- **template** - starts a new project using one of [our code templates](https://github.com/qcr/code_templates)

## The QCR Script

This `qcr` script is standalone and allows you to run the latest version of any of our internal QCR tools, at any time in the future.

### Installation

There is no need to clone this repo to utilise the `qcr` script. To install the script perform the following:

1. Open a terminal and cd into your user bin directory: `cd ~/bin/` -  see below if you don't have this directory
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

### Adding your own tools

Simply add a new bash script to the `./tools/` directory of this repository, and push it on the `master` branch. It will then be available for all users of the `qcr` script.

<br />
<br />
<br />

## Miscellaneous notes for QCR users

Below is an ad-hoc list of useful things for QCR members when using GitHub. The list may become more than a random brain dump as our utilisation of GitHub increases.

### Adding action files to your repositories

[GitHub Action](https://github.com/features/actions) files we think may be useful to QCR members are provided [here](https://github.com/qcr/tools/tree/master/github_actions).

The only one action currently is for automatically triggering an update of [https://qcr.github.io](https://qcr.github.io), but in the future actions may be added for publishing Python packages, generating Debian packages, and more.

To add an action to your repository simply paste the file in the `.github/workflows/` directory, make any edits requested in the Action file's comments, and push it to your `master` branch.

### Using the `qcrbot` GitHub account

We have a [qcrbot](https://github.com/qcrbot) GitHub account, which can be used to automate tasks within your repository. The account is linked to a QUT managed account, with full details available on a [private wiki page](https://wiki.qut.edu.au/display/cyphy/Shared+account+for+QCR+members). You must manually add the account to your repository due to its weakened security. It's important to consider the following:

- There is a repository token with write access to public repositories in plain-text below (it may be in a private repository, but sharing accidents happen...)
- You should ensure branch protection exists on your master branch to block any overwriting of your history (go to "settings" -> "branches" -> "add rule" and ensure "allow force pushes" is **unticked**)
- Many people have access to this account, don't give it any more permissions than it needs

Please see [this page](https://wiki.qut.edu.au/display/cyphy/Shared+account+for+QCR+members) on our private wiki if you would like to use access tokens in your scripts to automate use of the `qcrbot` account.
