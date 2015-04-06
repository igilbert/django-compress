# <font color='red'>django-compress is no longer maintained</font> #
Please consider switching to [django-pipeline http://django-pipeline.readthedocs.org/]!

This page is kept for historical reasons.

---

# Automated generation #
If `COMPRESS` and `COMPRESS_AUTO` is enabled (`True`), the source files will be automatically updated, and re-generated IF NEEDED when invoked from the templatetags. The last modified time of the files will be compared, and if any of the source-files is newer than the output-file, the file will be re-generated.

# Management command #
You can update and force updates of the compressed file(s) with the management command “synccompress”. This makes it possible to keep the files updated manually.

The command is
```
./manage.py synccompress
```
(assuming you are in you project-folder that contains `manage.py`). To force all files to be re-generated, use the argument `--force` (e.g. `./manage.py synccompress --force`)

# Templatetags #
django-compress includes two template tags: `compressed_css` and `compressed_js`, in a template library called `compressed`

They are used to output the 

&lt;link&gt;

 and 

&lt;script&gt;

-tags for the specified CSS/JavaScript-groups (as specified in the settings). The first argument must be the name of the CSS/JavaScript group.

The templatetags will either output the source filenames or the compressed filenames, depending on the `COMPRESS` setting, if you do not specify the `COMPRESS` setting, the source files will be used in DEBUG-mode, and compressed files in non-DEBUG-mode.
## Example ##
If you have specified the CSS-groups “my\_screen\_css” and “my\_print\_css” and a JavaScript-group with the name “my\_scripts”, you would use the following code to output them all:

```
{% load compressed %}
{% compressed_css 'my_screen_css' %}
{% compressed_css 'my_print_css' %}
{% compressed_js 'my_scripts' %}
```

# Far future Expires #
Far future Expires can be used with the `bump_filename`-option, see the [FarFutureExpires](FarFutureExpires.md) page for more information.