# Building-a-Python-package
By now, we have made use of some popular Python packages such as numpy and pandas. It's hard to find a data scientist who hasn't, at the very least, heard of either of these packages.
Requirements
Visual Studio Code IDE.
Install Git.
free GitHub account.
#### 1. Set up project working directory
Once all of the necessary software has been installed, we will need to set up our project working directory. Let's work through this process step by step to create our file structure and each of the files we will need.

#### File structure
The end goal of this tutorial is to make our package pip installable. For this to be possible, we will need to structure our files in a particular way.

#### Setup files
Now let's create our files. We will do this using the VS Code IDE we installed earlier.

Open up the VS Code text editor then click on Open... and navigate to and select the root folder, mypackage , which we created in the previous step.

VS Code has a built-in file browser that allows us to create new files and folders. The file browser is shown on the left side of our screen.

Our next step is to create two new folders within our project's root folder:

mypackage
tests

Within the mypackage folder, we create two Python files:

myModule.py : This is where we will write our function – the task we wish our package to do.
__init__.py : This is used so that Python knows the directory is a module.
Within the tests folder, we create one Python file:

test.py : This file will be our unit test, to ensure our module is working correctly before we publish our package.
Our project directory should now look like this:

#### 2. Build our package
Now that we have our folder structure set out, we can start writing some code! We will need to do three things:

Create our function.
Test our function.
Write some documentation for our package.
Create our function
The function we are going to create will perform the task of returning the top-n items in an array, in descending order. To do this, we will create an algorithm not too dissimilar to the Bubble sort algorithm.

#### Docstrings
All good programmers need to know how to write clean, concise, and descriptive docstrings for their functions.

Here is an example of a well-documented function:

def fibonacci(n):
​
    """
    Calculate nth term in fibonacci sequence
    
    Args:
        n (int): nth term in fibonacci sequence to calculate
    
    Returns:
        int: nth term of fibonacci sequence,
             equal to sum of previous two terms
    
    Examples:
        >>> fibonacci(1)
        1        
        >> fibonacci(2)
        1
        >> fibonacci(3)
        2
    """
​
    if n <= 1:
        return n
​
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)
Having this level of documentation will help anyone who uses your function to properly understand how the function works.

We'll do the same for our function. Add the following code into the myModule.py file:

def top_n(items, n):
    """Return the top n items in an array, in descending order.
​
    Args:
        items (array): list or array-like object containing numerical values.
        n (int): number of top items to return.
​
    Returns:
        array: top n items, in descending order.
​
    Examples:
        >>> top_n([8, 3, 2, 7, 4], 3)
        [8, 7, 3]
    """
    
    # We add the body of the function just below the docstring:
    
    for i in range(n):  # Keep sorting until we have the top n items
        for j in range(len(items)-1-i):
​
            if items[j] > items[j+1]:  # If this item is bigger than next the item..
                items[j], items[j+1] = items[j+1], items[j]  # swap the two!
                
    # Get last two items
    top_n = items[-n:]
    
    # Return in descending order
    return top_n[::-1]
# Check whether the function works
top_n([8, 3, 2, 7, 4], 3)
This is what it should look like in VS Code:

View of our code in VS Code
Now add the following to the __init__.py file.

Ensure that you save your files.


from . import myModule
Testing our package
It is good practice to write some tests for every function we create.

Why is this a good practice?

In test.py, add the following:

from mypackage import myModule
​
def test_top_n():
    """
    make sure top_n works correctly
    """
    
    assert myModule.top_n([8, 3, 2, 7, 4], 3) == [8, 7, 4], 'incorrect'
    assert myModule.top_n([10, 1, 12, 9, 2], 2) == [12, 10], 'incorrect'
    assert myModule.top_n([1, 2, 3, 4, 5], 5) == [5, 4, 3, 2, 1], 'incorrect'
Creating supporting files
Next, we will need to create another file named setup.py which describes our package. This setup file is what makes our package installable.

In our package's root directory, create setup.py and add the following code.

Replace the url, author, and author_email value fields with what is relevant to your package.

from setuptools import setup, find_packages
​
setup(
    name='mypackage',
    version='0.1',
    packages=find_packages(exclude=['tests*']),
    license='MIT',
    description='EDSA example python package',
    long_description=open('README.md').read(),
    install_requires=['numpy'],
    url='https://github.com/<username>/<package-name>',
    author='<Your Name>',
    author_email='<Your Email>'
)
Consult the table below for some additional information on the parameters in setup.py.

#### Parameter	Comments
name	The name package managers will use for your project, like numpy or pandas
version	The current version number of your project
license	Name of the license you chose
description	One-sentence description of your package
install_requires	List of all other packages this package depends on; package managers will install these automatically as needed
Lastly, we create a README.md file in our project's root folder. Here, we add anything we would like to describe our package in more detail.

Go to this website for some helpful info on how to make a proper README file.

Completed code in Atom
#### 3. Distribute our package
We are now ready to ship our package. Let's package it up and distribute it on GitHub.

#### Distribute to GitHub
We now want to publish our package so that anyone else can download and use it. This is done by publishing your package to GitHub.

What are some of the other ways to publish a Python package?

#### a) Initialise local Git repository
Using any terminal, we navigate to our project's root folder and issue the following commands, one line at a time.

git init
git add .
git commit -m "First commit"
#### b) Create remote repository
Log into GitHub and create a new repository.

The following image depicts this process, where the GitHub user 'James-Leslie' is creating a new repository. Ensure that your repository is marked as Public.


#### c) Push to GitHub
Copy the URL for the remote repository and issue the following commands.

The image below shows where you can obtain the URL.

git remote add origin <remoteURL>
git push origin master

#### 4. Install our package
We can now install our package onto any computer with internet access!

We issue the command below to install our package from GitHub.

Make sure to replace your-name and your-repo with the appropriate text.

pip install git+https://github.com/your-name/your-repo.git
If you need to install a later version of your package, then use:

pip install --upgrade git+https://github.com/your-name/your-repo.git
#### 5. Maintaining our package
We now have a version 0.1 of our first Python package! With this being done, we are in a position to make improvements and expand on its scope.

Package development workflow
We follow these steps when making changes to our package:

Make changes locally.
Push changes to GitHub.
Install updated version.
#### 1) Make changes locally
Your package consists of several interdependent files. It is important to keep all of these dependencies in check.

A likely workflow will look something like this:

add new functions, or improve existing functions
update test.py if needed
update __init__.py if needed
update setup.py if needed (make sure to update the version number)
Once we have tested our functions, and we are happy to push the new version, we run the same setup command as before:

python setup.py sdist
#### 2) Push changes to GitHub
When we are ready to publish our updated package, we follow the commands below:

git status
git add .
git commit -m 'make sure to include an appropriate commit message'
git push
#### 3) Install the updated version
The last step is to install our updated version, using the command below:

pip install --upgrade git+https://github.com/your-name/your-repo.git
