=============================
heroku-buildpack-multi-subdir
=============================

Use multiple buildpacks on your app with support of subdirectory

Fork of https://github.com/ddollar/heroku-buildpack-multi

Compared to the original project, it expects each dependency to be in a dedicated sub
directory.

Usage
=====

::

    $ heroku config:add BUILDPACK_URL=https://github.com/Stibbons/heroku-buildpack-multi-subdir.git

Example::

    $ cat .buildpacks
    subdir1=https://github.com/heroku/heroku-buildpack-nodejs.git#0198c71daa8
    subdir2=https://github.com/heroku/heroku-buildpack-ruby.git#v86
    https://github.com/emk/heroku-buildpack-rust

- First buildpack is executed as if the root were in the "subdir1" sub directory.
- Same for the second buildpack.
- The third one expect to be run at the root folder.

The ``.heroku`` and ``.profile.d`` directories of sub folders are merged.

License
=======

MIT
