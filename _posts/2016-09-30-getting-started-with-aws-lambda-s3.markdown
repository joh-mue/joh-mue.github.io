---
title: Getting started with programming for AWS, Lambda & S3
layout: post
categories: tech, aws, guide
---

It was time to dive into the jungle that is Amazon Web Services and since I did not find a good guide for my level of expertise I figured I should write one for others that that may come after me.

All this is done on on macOS 10.11
I use homebrew as the convenient tool to install and _uninstall_ missing software or packages.

In order to install it copy this command to your terminal

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

or got to [brew.sh](brew.sh) to find out more.

To get pip, pythons package manager, I installed python using

```
brew install python
```

This will install the latest verison of python which comes with pip.

_Note: Some version of python is already installed on each Mac but it does not come with pip - therefore the seemingly redundant installation of python._

Now that pip is installed you can get the necessary python packages and the aws command line interface which is used to access aws resources and to configure and store credentials to access aws resources.

```
pip install boto3
pip install awscli
```

That's your computer's preparation. Now you'll want to head over to the [aws.amazon.com](https://aws.amazon.com) and sign up for a developer account.

The bad news is, that you'll probably have to give some credit card information right away. The good news is that at the time of writing this amazon gives quite generous allowance to use and test their services. (As an example: you have 1 Million free AWS Lambda calls every month) So you won't actually have to pay anything until you start using AWS services quite heavily or of course if you screw up and somehow write a loop that accesses resources like crazy.

When you signed up, you can 

Alternatively have a look at [AWS BOTO3 Quickstart](https://boto3.readthedocs.io/en/latest/guide/quickstart.html)

... continued
