.. _contributedocs:

Contributing to Rockstor documentation
======================================

Steps for contributing to **rockstor-doc** repo are similar to contributing to
**rockstor-core**, as we follow the same fork and pull request model. We'll
assume you have basic proficiency with Git and are familiar with using a
text editor or IDE of your choice. Emacs, Vim, Eclipse and PyCharm are some
recommendations. Or you may be able to use an online such as https://livesphinx.herokuapp.com/. 
We'll further assume that you have your laptop ready with git
and an editor installed. Since we rely on github services, you need to create a
profile on github.com.

Once you have your profile set-up on github.com, follow these steps

Go to `rockstor-doc repo <https://github.com/rockstor/rockstor-doc>`_ and click
on the **Fork** button. This will fork the repository into your profile which
serves as your private git remote called origin. The next few git steps are
demonstrated on a Linux terminal. They work the same on a Mac too. Your IDE may
have ways to completely avoid the terminal, but using the terminal makes you
look cool.

.. code-block:: bash

        [you@your_laptop ~/projects]# git clone git@github.com:your_github_username/rockstor-doc.git

The above command creates a local **rockstor-doc** git repo in a new directory
by the same name(rockstor-doc). Change into it.

.. code-block:: bash

        [you@your_laptop ~/projects]# cd rockstor-doc

Configure this new git repo with your name and email address. This is required
to accurately record collaboration.

.. code-block:: bash

        [you@your_laptop rockstor-doc]# git config user.name "Firstname Lastname"
        [you@your_laptop rockstor-doc]# git config user.email your_email_address

Add a remote called upstream to periodically rebase your local repository with
changes in the upstream made by other contributors.

.. code-block:: bash

        [you@your_laptop rockstor-doc]# git remote add upstream https://github.com/rockstor/rockstor-doc.git


Making changes
--------------

We'll assume you have identified an issue(eg: #1234) from the `github issue
tracker <https://github.com/rockstor/rockstor-doc/issues>`_ to work on. If you
want to document something for which there is no issue, feel free to create
one.

First, start with the latest documentation by rebasing your local repo's master
branch with the upstream.

.. code-block:: bash

        [you@your_laptop rockstor-doc]# git checkout master
        [you@your_laptop rockstor-doc]# git pull --rebase upstream master

Checkout a new/separate branch for your issue. For example:

.. code-block:: bash

        [you@your_laptop rockstor-doc]# git checkout -b issue#1234_brief_label

You can then start making changes in this branch. Once done you can add your
changes.

.. code-block:: bash

        [you@your_laptop rockstor-doc]# git add new_file_added.rst existing_file.rst


We strongly encourage you to commit changes a certain way to help other
contributors and keep the merge process smooth. Below guidelines are more
pertinent to code contributions, but feel free to be as perfect as you like. As
a guiding principle, separate your changes into one or more logically
independent commits.

.. code-block:: bash

        [you@your_laptop rockstor-doc]# git commit new_file_added.rst existing_file.rst

We request that you divide a commit message into three parts. Start the message
with a single line summary, about 50-70 characters in length. Add a blank line
after that. If you want to add more than a summary to your commit message,
describe the change in more detail in plain text format where each line is no
more than 80 characters. This description should be in present tense. Below is
a fictional example:

.. code-block:: bash

        foobar functionality documentation for rockstor

        This document describes foobar functionality. This feature is based on algorithm called
        recursive transaction launcher to generate transactional foobars.

        # Please enter the commit message for your changes. Lines starting
        # with '#' will be ignored, and an empty message aborts the commit.
        # On branch issue#1234_test
        # Changes to be committed:
        #   (use "git reset HEAD <file>..." to unstage)
        #
        #       new file:   foobar.py
        #

If you'd like credit for your patch or if you are a frequent contributor, you
should add your name to the `rockstor-doc AUTHORS
<https://github.com/rockstor/rockstor-doc/blob/master/AUTHORS>`_ file.


Unlike for code contributions, there is no need for a build VM. We use `Sphinx
<https://www.sphinx-doc.org>`_ to generate the html content from .rst
files we edit. Installation procedure varies if you are on Mac, Windows, or Linux, so
follow the appropriate installation guide for Sphinx.


Installing Sphinx
^^^^^^^^^^^^^^^^^
In order to properly develop and submit contributions you'll need to install Sphinx, plus one Sphinx extension

`Sphinx official documentation <https://www.sphinx-doc.org/en/master/#>`_ gives guidelines for installating Sphinx on various platforms.
Details of how to install Sphinx is covered in their  `Installing Spinx <https://www.sphinx-doc.org/en/master/usage/installation.html>`_ documentation.

Once you have Sphinx installed you'll need 1 more Sphinx extensions before you're fully ready.
The sphinxcontrib-fulltoc package, generates the sidebar table of contents.

`sphinxcontrib-fulltoc <https://pypi.org/project/sphinxcontrib-fulltoc/>`_ generates detailed sidebar table of contents.

While you may not use the functionality of these extensions in your page, when you execute a *make html*
to check your work, you'll need these packages for the make to complete successfully.  
If you are generating videos, and prefer uploading your videos to the Rockstor Youtube channel,
please, send an email to support@rockstor.com

For a **Python 2** installation, use these commands.

.. code-block:: bash

        [you@your_laptop /path/to/rockstor-doc]# sudo pip install --user sphinxcontrib-fulltoc

For a **Python 3** installation, favoured, use these commands.

.. code-block:: bash

        [you@your_laptop /path/to/rockstor-doc]# sudo pip3 install --user sphinxcontrib-fulltoc


Using Sphinx as a Docker container
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Sphinx can also be used as a docker container, without needing to install it on your computer.
But the base image `docker-sphinx <https://github.com/sphinx-doc/docker>`_ doesn't contain **sphinxcontrib-fulltoc** which is needed by Rockstor documentation,
in order to add this package, you must build your own docker image.
This can be easily done by creating a simple :code:`Dockerfile` containing this:

.. code-block:: Dockerfile

        FROM sphinxdoc/sphinx

        WORKDIR /docs
        RUN pip3 install sphinxcontrib-fulltoc

Now you can just build the container with this command:

.. code-block:: bash

        [you@your_laptop /path/to/sphinx-rockstor]# docker build -t sphinx-rockstor .

Generating html files with Sphinx
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
As you edit the content in .rst files, you can periodically generate html files
and review them in your browser. To generate or update the HTML files, use the
following command :

.. code-block:: bash

        [you@your_laptop /path/to/rockstor-doc]# make html

If you use :code:`docker-sphinx` you can use the following command:

.. code-block:: bash

        [you@your_laptop /path/to/rockstor-doc]# docker run --rm -v $PWD:/docs sphinx-rockstor make html

HTML files are generated in _build/html directory. From a separate terminal
window, you can have a simple Python webserver always serving up this content
with one of the following commands:

For a **Python 2** installation, use the following command.

.. code-block:: bash

        [you@your_laptop /path/to/rockstor-doc/_build/html]# python -m SimpleHTTPServer 8000

For a **Python 3** installation, use the following command.

.. code-block:: bash

        [you@your_laptop /path/to/rockstor-doc/_build/html]# python -m http.server 8000

You can now go to :code:`https://localhost:8000` in your browser to review your
changes. The webserver is to be started only once and it will continue to serve
the files and changes you make to them.

After making any changes to a .rst file, run *make html* as shown above and
refresh your browser.

Once you are satisfied with changes and committed them to your branch following
the steps outlined here, you can open a pull request.

As you continue to work on an issue, commit and push changes to the issue
branch of your fork.  You can periodically push your changes to github with the
following command:

.. code-block:: bash

        [you@your_laptop ]# cd /path/to/rockstor-doc
        [you@your_laptop rockstor-doc]# git push origin your_branch_name

When you finish work for the issue and are ready to submit, create a pull
request by clicking on the **pull request** button on github. This notifies the
maintainers of your changes. As a best practice only open one pull request per
issue containing all relevant changes.

When you are ready, open the pull request and please follow these 2 tips to expedite the review:

* When you've finished your edit, run the Sphinx :code:`make html` command, and
  paste its output into the pull request discussion string to help speed up the
  review. After you've generated the html, you can use the webserver detailed
  above to check the functionality of your work prior to your pull request.

* When you make a pull request, adding a "Fixes #number-of-issue" on its own
  line will automatically close the related issue when it gets merged. Just a
  nice thing to have and also provides a link to the relevant issue. See
  `GitHub documentation <https://docs.github
  .com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue>`_ for details.
