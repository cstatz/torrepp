# How to contribute
We love third-party contributions to torrepp. This can be anything from enhanced 
documentation, bug fixes in general or fixes for your specific platform. 

When contributing to this repository, please first discuss the change you wish 
to make via issue with us of this repository before making a change.

Following are some general guidelines to increase the chance of successfully 
contributing.

## Creating Issues
If you come across any problem, we would like to know about it. Also, if you would like to 
see a specific feature in torrepp, create an issue to discuss the feature. 

Currently, there are two templates for bugs and feature requests. If you feel that your issue
does not fit either criteria, feel free to open an issue anyway.

We will try to get back to you as soon as possible.

## Pull Requests
We love pull requests from everyone to make sure that torrepp is as good as possible.
Before creating a pull request for anything major, please file an issue to make us aware 
of your intended work. If your pull request is a bug fix or introduces a new feature, 
please reference the issue in your pull request.

Fork, then clone the repo:
```shell script
git clone git@github.com:your-username/torrepp.git
```
Set up the build directories and build torrepp:
```shell script
mkdir build
cd build 
cmake ../
cmake --build .
```
Run the tests and check that everything is setup correctly:
```shell script
ctest
```
Now **make your changes** and if necessary **add tests** to ensure proper functionality. 
Run them before pushing to your fork.

If everything work as you desire, push to your fork and [submit a pull request][pr].

[pr]: https://github.com/cstatz/torrepp/compare/

Now it's on us to check your code. We try to do this as quickly as possible.

Some things that will increase the chance that your pull request is accepted:

* Write tests.
* Run the provided clang-format file on the code
* Write a [good commit message][commit].

[commit]: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
