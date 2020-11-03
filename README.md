# QCR shared tools

This repository contains useful **PRIVATE** tools for use by members of QCR. Please consider carefully how you use them, who you share them with, and what you put in your public repositories (including their history!).

Below is an ad-hoc list of useful things for QCR members when using GitHub. The list may become more formalised as our utilisation of GitHub increases.

## Adding action files to your repositories

[GitHub Action](https://github.com/features/actions) files we think may be useful to QCR members are provided [here](https://github.com/qcr/tools/tree/master/github_actions).

The only one action currently is for automatically triggering an update of [https://qcr.github.io](https://qcr.github.io), but in the future actions may be added for publishing Python packages, generating Debian packages, and more.

To add an action to your repository simply paste the file in the `.github/workflows/` directory, make any edits requested in the Action file's comments, and push it to your `master` branch.

## Using the `qcrbot` GitHub account

We have a [qcrbot](https://github.com/qcrbot) GitHub account, which can be used to automate tasks within your repository. The account is linked to a QUT managed account, with full details available on a [private wiki page](https://wiki.qut.edu.au/display/cyphy/Shared+account+for+QCR+members). You must manually add the account to your repository due to its weakened security. It's important to consider the following:

- There is a repository token with write access to public repositories in plain-text below (it may be in a private repository, but sharing accidents happen...)
- You should ensure branch protection exists on your master branch to block any overwriting of your history (go to "settings" -> "branches" -> "add rule" and ensure "allow force pushes" is **unticked**)
- Many people have access to this account, don't give it any more permissions than it needs

Please see [this page](https://wiki.qut.edu.au/display/cyphy/Shared+account+for+QCR+members) on our private wiki if you would like to use access tokens in your scripts to automate use of the `qcrbot` account.
