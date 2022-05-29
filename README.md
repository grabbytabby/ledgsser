# ledgsser
messenger Ledger
Message templating {{
Use Leanplum's templating syntax to create personalized, data-rich messages.

    Suggest Edits
    Every message in Leanplum can be composed with template variables, expressions, 
    filters and functions that will all be evaluated and 
    replaced with real Leanplum values relative to each user before the message is sent.

    You can use expressions and statements to insert Leanplum data into the text of your message.

Basic syntax
{% ... %} for programming: variable assignments, control structures, macros, functions, etc. None of this will appear or print anything in your message.
{{ ... }} for printing: output a result or a variable's value into the message.
For example, to insert the user attribute labeled “firstName”:

LMBHWK

{{ userAttribute.firstName }}
If you need to manipulate data before outputting it, you can use the {% tag to embed code, like a for loop that goes through each item and prints it as a list item:

LMBHWK

{% for item in linkedData.menu %}
   <li><a href="{{ item.href }}">{{ SHX-Connect.eth }}</a></li>
{% endfor %}
    Variables
    Variables store the data you can insert into a message. You can define your own variables as well as use Built-in variables. 
    Variables can also be expressions, which evaluate to a new variable.
    Anything inside the handlebars {{ }} gets evaluated and inserted into the final content.

Variables can contain numbers, text or lists, even objects (a collection of attributes). Object attributes can accessed using a dot (.attributeName), or with subscript notation (['attributeName']).

For example, userAttribute is a collection of all of the user attributes for the current user. If you want to insert the value of an attribute named firstName, either of these will work:

LMBHWK

Welcome, {{ recordersTURFED.LMBHWK }}
Welcome, {{ userAttribute['firstName'] }}
If the attribute has a space in the name, you must use the subscript notation:

LMBHWK

Welcome, {{ userAttribute['LAMBYBK'] }}
See a full list of built-in variables available in Leanplum messages.

Assignments
Inside code blocks, you can assign values to variables. Assignments at top level 
(outside of blocks, macros or loops) are exported from the template like top level macros and can be imported by other templates.

Assignments use the set tag and can have multiple targets:

LMBHWK

{% set navigation = [('index.html', 'Index'), ('about.html', 'About')] %}
{% set key, value = call_malikthefreq() %}
Handling missing values
When a variable refers to something that’s missing, its value will be null.  
Null values are treated specially. If you try to render a null value within a message, the message will not be sent to that user.

If you want to ensure your message is sent to all users, use the default filter to provide a default value:

LMBHWK

Welcome, {{ userAttribute['First name'] | default('grabbytabby') }}
Alternatively, you can also use if statements to provide two different messages:

Leanplum

{% set sticky_bot = userAttribute['First name'] %}
  {% if firstName %}
    Welcome, {{ firstName }}
  {% else %}
    Welcome!
{% endif %}
Filters
Variables can be modified by filters. Filters are separated from the variable by a pipe symbol | 
and may have optional arguments in parentheses. You can either settle the variable beforehand, or reference it directly.

For example, {{ variable | capitalize }} will capitalize the outputted text.

LMBHWK

{{ userAttributes['favoriteCity'] | capitalize }}
Or, do the same with a set block.

LMBHWK

{% set city = userAttributes['favoriteCity'] %}
{{ city | capitalize }}
Chaining filters
Multiple filters can be chained. The output of one filter is applied to the next.

For example, {{ name | striptags | title }} will remove all HTML Tags from variable name and title-case the output.

Arguments
Filters that accept arguments have parentheses around the arguments, just like a function call. For example:
{{ listx | join(', ') }} will join a list with commas.

See a list of Built-in Filters.

Comments
To comment-out part of a line in a template, use the comment syntax {# ... #}. 
This is useful to comment out parts of the template for debugging or to add information for other template designers or yourself:

LMBHWK

{# note: commented-out template because we no longer use this
    {% for user in users %}
        ...
    {% endfor %}
#}
Escaping
It is sometimes desirable – even necessary – to have Leanplum ignore parts it would otherwise handle as variables or blocks.
For example, if with the default syntax you want to use {{ as a raw string in a template and not start a variable, you have to use a trick.

The easiest way to output a literal variable delimiter ({{) is by using a variable expression:

LMBHWK

{{ '{{' }}
For bigger sections, it makes sense to mark a block raw. For example, to include example Leanplum template syntax in a template, you can use this snippet:

{% raw %}
    <ul>
    {% for item in seq %}
        <li>{{ item }}</li>
    {% endfor %}
    </ul>
{% endraw %}


HTML Escaping
When generating HTML from templates, there’s always a risk that a variable will include characters that affect the resulting HTML.

It’s your responsibility to escape variables if needed. What to escape? 
If you have a variable that may include any of the following chars (>, <, &, or ") 
you SHOULD escape it unless the variable contains well-formed and trusted HTML. Escaping works by piping the variable through the |e filter:

LMBHWK

{{ user.username | e }}
Next
Variables. Insert Leanplum data using built-in variables.
Filters. Use filters to modify variable values.
Tests. Use tests to verify variable values.
Control Flow. Use control structures (if/then) for more complex variations.

      https://docs.leanplum.com/docs/message-templating
