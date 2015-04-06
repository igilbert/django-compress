# <font color='red'>django-compress is no longer maintained</font> #
Please consider switching to [django-pipeline http://django-pipeline.readthedocs.org/]!

This page is kept for historical reasons.

---

Installation is pretty straight-forward and follows the same installation procedure as many other Django applications. django-compress does not create any models, so you do not need to configure a database.

## Recommendations ##
By default django-compress uses CSSTidy to compress CSS. CSSTidy is an excellent stand-alone application for dealing with CSS-files. CSSTidy can be downloaded from: http://csstidy.sourceforge.net/. If you do not install CSSTidy, make sure to disable the filter in your settings (by setting COMPRESS\_CSS\_FILTERS = None).

## Install instructions ##
  1. Get the code from svn: `svn co http://django-compress.googlecode.com/svn/trunk/ django-compress`
  1. 
    1. Use the `setup.py` script to install: `python setup.py install`
    1. OR manually put the `compress`-directory somewhere on your PYTHONPATH
  1. Add `'compress'` to your INSTALLED\_APPS

## Using git? ##
The main source repository is now available at github: http://github.com/pelme/django-compress/tree/master

The Subversion repository at Google Code will still be updated, though.

If you want to grab django-compress via git, use:
`git://github.com/pelme/django-compress.git`