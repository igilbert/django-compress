# <font color='red'>django-compress is no longer maintained</font> #
Please consider switching to [django-pipeline http://django-pipeline.readthedocs.org/]!

This page is kept for historical reasons.

---


django-compress can be customized an a couple of ways.

If you need to change the output of the HTML-tags generated from the templatetags, this can be done by overriding the templates `compress/css.html` and `compress/js.html`.

You can also write your own filter-class, if you for example want to implement other types of compressors. All you need to do is to define a filter\_css and/or a filter\_js functions in a class that inherits from `compress.filter_base.FilterBase`, and specify it in the tuple of filters (`COMPRESS_CSS_FILTERS`/`COMPRESS_JS_FILTERS`) (see [Configuration](Configuration.md) for more information) in the settings.

For now, see the files under [filters/](http://django-compress.googlecode.com/svn/trunk/filters/) for more details. CSSTidyFilter uses and external program, and JSMinCompressor just calls a Python-function, so it will probably be able to point you in the right direction when writing custom filters.