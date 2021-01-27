# Coding style guide

The intention with this style guide, as with the other guides, is to provide a common framework between the developers within our team so that we can work together more efficiently. None of these rules are set in stone, but are open to modification and interpretation from all the developers.

For the most part, we will be using the common style guide for each coding language in which we write our code. Beyond that, we will be using the EditorConfig plugin for our text editors. If you prefer to use a console-based editor like vim, emacs, or nano, it may be a bit more involved to install the EditorConfig plugin, so if you like, you can just view the .editorconfig file and try to follow the guidelines. In the [mac-dev-setup](https://github.com/rgutierrez-cotech/mac-dev-setup) repository that’s used for setting up your computer for development, you can find the .editorconfig file that we’ll be using. Download it to your machine, install the EditorConfig plugin for your text editor, and copy the .editorconfig file into your project directory. You’ll need to copy it into every project you work on.

Finally, here are some general guidelines to follow:

* Try to write docstrings for your functions as you go along, using the language’s suggested format. Use your best judgement to determine if the function is clear enough or if docstrings or inline comments are necessary.
* When writing comments, don’t let the line length exceed 65 characters. If the line will exceed 65 characters, insert a line break and continue the comment below.
* When writing a particularly lengthy function call, if statement, loop, etc., break it up into multiple lines and make sure you double-indent the lines of the call or statement. This physically separates the statement from the rest of the code below. Here is an example:
```
# Instead of this:

if (a == request.params.get('a') && b == 
    request.params.get('b') && c < d.getProduct())
    print "a and b"
endif
```
```
# Do this:

if (a == request.params.get('a') && 
        b == request.params.get('b') && 
        c < d.getProduct())
    print "a and b"
endif
```
```
# Another example:

next_page = self.get_next_page(survey_id, \
        left_off_at, \
        page_order, \
        current_respondent, \
        item_responses)
```

* Use TODOs and FIXMEs when necessary

**PHP**

* Make sure there are spaces between parentheses, brackets, and in expressions between variables and operators
```
function test_func( $arg1, $arg2 ) {
    if ( $arg1 > $arg2 ) {
        return $arg1;
    } else {
        return $arg2;
    }
}
```

* Always use the full `if` notation with brackets, *unless* you are using the ternary operator, like below:
```
x < 5 ? echo 'small' : echo 'big';
```