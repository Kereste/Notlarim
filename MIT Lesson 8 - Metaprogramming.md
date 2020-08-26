<h1>Lecture 8: Metaprogramming</h1>
<strong>Source:</strong> https://missing.csail.mit.edu/2020/metaprogramming/ <br>

<h2>Semantic Version</h2>
8.1.7<br>
│ │ └─> Patch Version<br>
│ └─> Minor Version<br>
└─> Major Version<br>

<h3>Major Version</h3>
Increment if you make a backwards incompatible change. 
Where if my software used to work with whatever version you had and then you make a change that 
means that my software might no longer work such as removing a function or renaming it.
Then you increment the major version and set minor and patch versions to zero.

<h3>Minor Version</h3>
If you add something to the library, 
you increment the minor version and you set the patch version to zero.

<h3>Patch Version</h3>
* Change you made is entirely backwards compatible 
* It does not add or remove anything
* It does not rename anything externally
* It is as if nothing changed,
then you only increment the patch number.

<h2>Continuous Integration Systems</h2>
Continuous integration, or CI, is an umbrella term for “stuff that runs whenever your code changes”, and there are many companies 
out there that provide various types of CI, often for free for open-source projects. 
Some of the big ones are Travis CI, Azure Pipelines, and GitHub Actions. 
They all work in roughly the same way: you add a file to your repository that describes what should happen when various 
things happen to that repository. By far the most common one is a rule like “when someone pushes code, run the test suite”. 

<h2>Tests</h2>

    Test suite: a collective term for all the tests
    Unit test: a “micro-test” that tests a specific feature in isolation
    Integration test: a “macro-test” that runs a larger part of the system to check that different feature or components work together.
    Regression test: a test that implements a particular pattern that previously caused a bug to ensure that the bug does not resurface.
    Mocking: to replace a function, module, or type with a fake implementation to avoid testing unrelated functionality. For example, you might “mock the network” or “mock the disk”.


<h2>Misc</h2>
**Lock File**<br>
When working with dependency management systems, you may also come across the notion of lock files. 
A lock file is simply a file that lists the exact version you are currently depending on of each dependency. 
Usually, you need to explicitly run an update program to upgrade to newer versions of your dependencies. 
There are many reasons for this, such as avoiding unnecessary recompiles, having reproducible builds, or not automatically updating to the latest version (which may be broken). 

**Vendoring**<br>
An extreme version of this kind of dependency locking is vendoring, which is where you copy all the code of your dependencies into your own project. 
That gives you total control over any changes to it, and lets you introduce your own changes to it, 
but also means you have to explicitly pull in any updates from the upstream maintainers over time.

