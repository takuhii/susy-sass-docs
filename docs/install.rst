Getting Started
===============

Susy-sass runs on `Dart Sass`_, the current, actively-maintained Sass
implementation. The old `Node-sass`_/`Compass`_ Ruby toolchain is no longer
required (or supported).

You need two things:

- `Dart Sass`_ (the ``sass`` package), and
- Susy-sass itself.

.. _Dart Sass: https://sass-lang.com/dart-sass/
.. _Node-sass: https://sass-lang.com/blog/libsass-is-deprecated/
.. _Compass: http://compass-style.org/


Install with npm
----------------

Install Susy-sass and Sass as dev dependencies:

.. code-block:: bash

  # command line
  npm install susy-sass --save-dev
  npm install sass --save-dev

.. note::

  The current ``sass`` release requires Node.js 20.19 or newer. Susy-sass
  declares this through its ``engines`` field, so older Node versions will be
  flagged on install.


Usage
-----

Susy-sass ships two entry points, so you can use either the legacy ``@import``
syntax or the modern ``@use`` syntax.

Modern syntax (``@use``)
~~~~~~~~~~~~~~~~~~~~~~~~~

The recommended approach on Dart Sass. Import the namespaced ``susy-modern``
entry point:

.. code-block:: scss

  @use "susy-modern" as susy;

  .container {
    @include susy.container();
  }

  .span {
    @include susy.span(3 of 12);
  }

Legacy syntax (``@import``)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Still supported, and useful for upgrading existing projects:

.. code-block:: scss

  @import "susy";

  .container {
    @include container();
  }

  .span {
    @include span(3 of 12);
  }

.. warning::

  ``@import`` is deprecated in Dart Sass and will be removed in Dart Sass 3.0.0.
  It continues to work for now, but new projects should prefer the ``@use``
  syntax above.


Resolving the import path
-------------------------

How the ``susy`` / ``susy-modern`` names resolve depends on your build tool.

Sass CLI
~~~~~~~~

Add ``node_modules`` to the load path:

.. code-block:: bash

  # command line
  sass --load-path=node_modules src/app.scss dist/app.css

Then import by package name:

.. code-block:: scss

  @use "susy-modern" as susy;

Webpack (sass-loader)
~~~~~~~~~~~~~~~~~~~~~~

Install ``sass`` and ``sass-loader``:

.. code-block:: bash

  # command line
  npm install sass sass-loader --save-dev

Make sure ``sass-loader`` is enabled in your ``webpack.config.js``:

.. code-block:: js

  // webpack.config.js
  module: {
    rules: [
      {
        test: /\.scss$/,
        use: ['style-loader', 'css-loader', 'sass-loader'],
      },
    ],
  }

Then import (the ``~`` prefix resolves from ``node_modules``):

.. code-block:: scss

  /* app.scss */
  @use "~susy-sass/sass/susy-modern" as susy;

Gulp
~~~~

.. code-block:: js

  // gulpfile.js
  const sass = require('gulp-sass')(require('sass'));

  gulp.task('sass', function () {
    return gulp
      .src('scss/*.scss')
      .pipe(
        sass({ includePaths: ['node_modules'] }).on('error', sass.logError)
      )
      .pipe(gulp.dest('dist/css'));
  });


Manual Start
------------

If you would rather skip package management, you can copy the Sass files in
directly:

- Download the source from `GitHub`_.
- Copy the contents of the ``sass`` folder into your project.
- Import it with a relative path, e.g. ``@use "susy/susy-modern" as susy;``.

.. _GitHub: https://github.com/takuhii/susy-sass


Quick Start
-----------

Once Susy-sass is imported, the basic layout is composed with two mixins:

.. code-block:: scss

  @use "susy-modern" as susy;

  .page { @include susy.container(80em); }  // establish a layout context
  .nav  { @include susy.span(3 of 12); }    // lay out your elements

You don't have to do things the Susy way, though. Susy gives you direct access
to the math, so you can use it however you like:

.. code-block:: scss

  @use "susy-modern" as susy;

  main {
    float: left;
    width: susy.span(4);
    margin-left: susy.span(2) + susy.gutter();
    margin-right: susy.gutter();
  }

You can also establish :doc:`global settings <settings>` by creating a
``$susy`` map:

.. code-block:: scss

  $susy: (
    columns: 12,   // The number of columns in your grid
    gutters: 0.25, // The size of a gutter relative to a single column
  );

There are many more settings for customizing every aspect of your layout —
keep going for the details.
