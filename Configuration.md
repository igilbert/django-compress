# <font color='red'>django-compress is no longer maintained</font> #
Please consider switching to [django-pipeline http://django-pipeline.readthedocs.org/]!

This page is kept for historical reasons.

---


See BackwardsIncompatibleChanges

# Specifying files #
You specify groups of files to be compressed in your settings. The basic syntax for specifying CSS/JavaScript groups files is:
```
COMPRESS_CSS = {
    'group_one': {
        'source_filenames': ('css/style.css', 'css/foo.css', 'css/bar.css'),
        'output_filename': 'css/one_compressed.css',
        'extra_context': {
            'media': 'screen,projection',
        },
    },
    
    # other CSS groups goes here
}

COMPRESS_JS = {
    'all': {
        'source_filenames': ('js/jquery-1.2.3.js', 'js/jquery-preload.js', 'js/jquery.pngFix.js',
        'js/my_script.js', 'js/my_other_script.js'),
        'output_filename': 'js/all_compressed.js',
    }
}
```
### Group options ###
  * `source_filenames` is a tuple with the source files to be compressed. The files are concatenated in the order it is specified in the tuple. This option is required.
  * `output_filename` is the filename of the (to be) compressed file. This option is required.
  * `extra_context` is a dictionary of values to add to the template context, when generating the HTML for the HTML-tags with the templatetags. This option is not required and can be left out. For CSS, if you do not specify `extra_context`/`media`, the default media in the `<link>` output will be `media="all"`.

Note that all filenames are specified relative to MEDIA\_ROOT, and thus the source files needs to be in your MEDIA\_ROOT.

# Other settings #
  * `COMPRESS`: When `COMPRESS` is `True`, CSS and JavaScripts will be concatenated and filtered. When `False`, the source-files will be used instead. Defaults to `not DEBUG` (compressed files will only be used in non-DEBUG-mode (production))
  * `COMPRESS_AUTO`: Auto-generate CSS and JavaScript files whenever needed, when the template tags are invoked. This setting will make sure that the outputted files always are up to date (assuming that you are using the provided templatetags to output the links to your files). If you disable this, you can use the management command to keep your files manually updated. Defaults to `True`.
  * `COMPRESS_VERSION`: regulates whether or not to add a "version number" to the outputted files filename with for use with “far future Expires”. For more information, see [FarFutureExpires](FarFutureExpires.md). When you specify `COMPRESS_VERSION` you will also need to add a placeholder (which by default is '?') for the version number in the `output_filename` setting. Files with new filenames will be generated if needed, and old outdated files will be removed at the same time. All files with a matching name e.g. `output_filename` where ? can be replaced by digits will be removed. If you for some reason have files named in the same way, you should consider moving them or putting the compressed files in their own directory.

`COMPRESS_VERSION` Example:
```
COMPRESS = True
COMPRESS_VERSION = True
COMPRESS_CSS = {
    'screen': {
        'source_filenames': ('css/screen/style.css', 'css/screen/paginator.css', 'css/screen/agenda.css', 'css/screen/weather.css', 'css/screen/gallery.css', ),
        'output_filename': 'c/screen.r?.css',
    },
}
```

This will output a file like /media/c/screen.[r1213947531](https://code.google.com/p/django-compress/source/detail?r=1213947531).css, which will be re-generated and updated when you change your source files.

  * `COMPRESS_CSS_FILTERS`: A tuple of filters to be applied to CSS files. Defaults to `('compress.filters.csstidy.CSSTidyFilter', )`. Please note that in order to use CSSTidy, you need to install CSSTidy (see [Installation](Installation.md) for more details).
  * `COMPRESS_JS_FILTERS`: A tuple of filters to be applied to JavaScript files. Defaults to `('compress.filters.jsmin.JSMinFilter',)`

`COMPRESS_*_FILTERS` can be set to an empty tuple or None to not use any filters. The files will however still be concatenated to one file.

## CSSTidy settings ##
If you choose to use CSSTidy (which is enabled by default), you can also use the following settings:
  * `CSSTIDY_BINARY`: name or path of the CSSTidy binary to be used for processing JavaScript-files with the CSSTidy filter. Defaults to `'csstidy'`.
  * `CSSTIDY_ARGUMENTS`: specifies arguments to be passed to CSSTidy. Defaults to `'--template=highest'`. See CSSTidy man-page or website for more details.

## YUI Compressor settings ##
  * `COMPRESS_YUI_BINARY`: command line to execute for the YUI program. Defaults to `'java -jar yuicompressor.jar'`. You will most likely change this to the location of yuicompressor on your system.
  * `COMPRESS_YUI_CSS_ARGUMENTS`: Additional arguments to use when compressing CSS. Defaults to `''`.
  * `COMPRESS_YUI_JS_ARGUMENTS`: Additional arguments to use when compressing JavaScript. Defaults to `''`.