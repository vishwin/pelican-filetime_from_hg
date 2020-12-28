filetime from hg: A Plugin for Pelican
====================================================

[![Build Status](https://img.shields.io/github/workflow/status/pelican-plugins/filetime-from-hg/build)](https://github.com/pelican-plugins/filetime-from-hg/actions)
[![PyPI Version](https://img.shields.io/pypi/v/pelican-filetime-from-hg)](https://pypi.org/project/pelican-filetime-from-hg/)
![License](https://img.shields.io/pypi/l/pelican-filetime-from-hg?color=blue)

If your blog content is versioned via Mercurial, this plugin will set articles' and pages' `metadata['date']` and `metadata['modified']` to correspond to that of the hg commit.  This plugin depends on the [`python-hglib` python package](https://www.mercurial-scm.org/wiki/PythonHglib).

Installation
------------

This plugin can be installed via:

    python -m pip install pelican-filetime-from-hg

Usage
-----

The date is determined via the following logic:

* if a file is not tracked by hg, or a file is added but never committed
    * `metadata['date']` = filesystem time
    * `metadata['modified']` = filesystem time
* if a file is tracked, but no changes in working directory
    * `metadata['date']` = first commit time
    * `metadata['modified']` = last commit time
* if a file is tracked, and has changes in working directory
    - `metadata['date']` = first commit time
    - `metadata['modified']` = filesystem time

When this module is enabled, `date` and `modified` will be determined by `hg status`; no need to manually set in article/page metadata. And operations like copy and move will not affect the generated results.

If you don't want a given article or page to use the hg time, set the metadata to `hgtime: off` to disable it.

You can also set `HG_FILETIME_FOLLOW` to `True` in your settings to make the plugin follow file renames — i.e., ensure the creation date matches the original file creation date, not the date it was renamed.

Contributing
------------

Contributions are welcome and much appreciated. Every little bit helps. You can contribute by improving the documentation, adding missing features, and fixing bugs. You can also help out by reviewing and commenting on [existing issues][].

To start contributing to this plugin, review the [Contributing to Pelican][] documentation, beginning with the **Contributing Code** section.

[existing issues]: https://github.com/pelican-plugins/filetime-from-hg/issues
[Contributing to Pelican]: https://docs.getpelican.com/en/latest/contribute.html

License
-------

This project is licensed under the AGPL-3.0 license.
