## User Guide

<sup>[[Japanese Edition](https://github.com/ayatakesi/neutriNote/blob/master/index.md)]</sup>

### <a name="toc">Table of Contents</a>

1. [Getting Started](#started)
1. [Backup and Restore](#backup)
1. [Mirror](#mirror)
1. [Search Tools](#search)
1. [Advanced Features](#advanced)
    * [Metadata](#metadata)
    * [Markdown](#md)
    * [Examples](#examples) 
    * [Automation](#automation)
    * [Text Expansion](#textexpansion)
    * [Tag Expansion](#tagexpansion)
    * [Batch Select](#batchselect)
    * [Voice Memo](#voicememo)
    * [External Fonts](#externalfonts)
    * [Ambient Glow](#ambientglow)
    * [Keyboard](#keyboard)
    * [Gestures](#gestures)
    * [Hacks](#hacks)
    * [Built-in Variables](#builtinvariables)
    * [Custom Variables](#customvariables)
    * [Storage Saver](#storage)
    * [API](#api)
    * [Python Support](#python)
    * [In-note JavaScript](#javascript)
    * [Web Components](#components)
    * [Diagrams](#diagrams)
    * [Text Editor](#texteditor)
    * [Editorless Read/Write](#editorless)
    * [Snooze](#snooze)
    * [Launcher Shortcuts](#launchershortcuts)
    * [Misc.](#misc)
1. [Performance](#performance)
1. [Log Tool](#log)
1. [Encryption](#encryption)
1. [OCR](#ocr)
1. [Relocate Local Repository](#relocate)
1. [Known Issues](#issues)
1. [FAQs](#faq)
1. [Privacy Policy](#privacy)
1. [TODO](#todo)
1. [Source Code](#source)
1. [About](#about)

### <a name="started">Getting Started</a>
Thank you for choosing **neutriNote**.  

Right after installation, be sure to follow the onscreen instruction and choose a location for **Local Repository**.  

If your repository is empty, you may add notes right away.  

If you have installed **neutriNote** previously, you may pick the repository already on your device.  

If you have settings backed up from your previous installation, you may also choose [Restore App Data](https://www.dropbox.com/s/nveejx2dn1pdbqi/navigation_drawer.png?dl=0, "Backup/Restore App Data") to restore settings.

To enable sync is easy, either install a third party app like [Syncthing](https://play.google.com/store/apps/details?id=com.nutomic.syncthingandroid&hl=en) and register your repository with it or get [neutriNote Connector+](https://play.google.com/store/apps/details?id=com.appmindlab.connectorplus) -- a Dropbox adapter designed just for 
**neutriNote**.  

Even without add-ons, **neutriNote** is ready for use.  Explore around to discover many features that would make **neutriNote** a highly integrated part of your note taking experience (for example, long tap metadata label to retrieve notes sharing [similar](https://www.dropbox.com/s/tqa3h774xrn49zd/metadata_long_click.png?dl=0) label and tap the local find icon in the edit screen to jump to the next match).  To extend it into a tool for personal information management, please do take a moment to go over the following sections.  New users may also want to check out [Backup and Restore](#backup) for ways to preserve note data beyond the sync mechanism.

**IMPORTANT**: from v1.3.1, **neutriNote** supports **Runtime Permissions** in Android Marshmallow devices.  Be sure to grant **neutriNote** permission to access external storage for its **Local Repository** to work properly.  To enable previously denied permissions, go to **neutriNote**'s **App Info** under Android, renable the permissions and restart the app.


### <a name="backup">Backup and Restore</a>
If you have already activated **Local Repository**, your notes will be sync seamlessly to the repository.  You can replicate your notes remotely by sharing the folder with third party apps such as [Syncthing](https://play.google.com/store/apps/details?id=com.nutomic.syncthingandroid&hl=en).  **IMPORTANT**: Do NOT use stale repositories since they could be out of sync.  Always use the method described in the [Getting Started](#started) section from above to initialize and assign repositories.
    
**Incremental Backup** is another way to copy your notes in non-intrusive fashion. To enable, simply do so from Settings.  Then your notes and app settings will be backed up incrementally at least once daily to a internal storage folder called _neutrinote_export_.  Note: exported app settings data are stored in regular notes with prefix _~neutrinote_ so that they can be sync no differently from other notes.

When incremental backup is enabled, a task to conduct full backup when the device is idle will also be activated.  A maximum of 10 most recent backups will be maintained.  See [Storage Saver](#storage) section for more suggestions on how to manage backup storage space.

If you are looking for instructions on how to transfer **Mirror** between installations, see the next section.

<a href="#toc">🔝 Back to top</a>


### <a name="mirror">Mirror (v3.3.1 or above)</a>

**Mirror** is a replica of **Local Repository** much like a **Remote Repository** for __push and pull__ local and remote changes.  The primary difference between **Local Repository** and **Mirror** is that in Android 11 access to the former is restricted for privacy reasons, while the later is accessible to 3rd party apps, such as [peer-to-peer sync](https://play.google.com/store/apps/details?id=com.nutomic.syncthingandroid) or a secondary text editor.  Thus **Mirror** is offered as an option depending on your privacy preferences and workflow.  To activate the feature, simply add a folder under [backup folder](#backup) and name it `mirror`, **Mirror Files** will appear under the main note list menu with options to __push__ and __pull__ changes. 

Note that only deletions initiated from **neurtiNote** (i.e. **Local Repository**) will be mirrored.  

```
📂 Backup
    |__ 📁 mirror
    |__ 📁 ...
    |__ 📁 ...
    |__ 📁 ...
```

To reconnect **neutriNote** to an existing **Mirror**, follow these steps:

1. Make sure you have updated **neutriNote** to v4.2.2 or above.
1. **IMPORTANT**: With the use of a file manager app, temporarily rename the `mirror` folder to something other than `mirror`.
1. Make sure **~neutrinote_settings_data.txt** and **~neutrinote_app_data.txt** are not empty.
1. Under **Settings**, disable **Auto Backup**.
1. Tap **Import Files** under the &vellip; main menu .  Choose the renamed folder in Step 2.
1. Wait for the import to complete.
1. Upon completion, click **Restore App Data** from the side navigation menu.
1. Revert the name of the folder back to `mirror`.
1. Under **Settings**, enable **Auto Backup**. 

Note: certain devices might be blocking your access to the &vellip; main menu in that **Import Files** would not be accessible when the note list is empty.  As a work around, by adding a note will usually make the menu accessible. 

<a href="#toc">🔝 Back to top</a>


### <a name="search">Search Tools</a>
While notes can be retrieved based on modified time, accessed time, and location as providied by the user interface, **neutriNote** supports high precision text based search and [regular expression](http://en.m.wikipedia.org/wiki/Glob_(programming)).  The syntax below are also highly reusable when they are included as part of the preset filters (under Settings).

**Search by Fields** It is possible to restrict search to a specified field.  For example, at the main search bar over the note list, search can be limited to titles by using the prefix `title:` in the search string.  A search string like`title:log` will return all notes with the substring `log` in the titles.  To apply [regular expression](http://en.m.wikipedia.org/wiki/Glob_(programming)) in title search, use the prefix `titlereg:`.

Search can also be limited to metadata by using the prefix _meta:_ in the search string.  A search string such as _meta:personal_ will return all notes with the substring _personal_ in the metadata (likewise _meta:_ will return notes without metadata). It is also possible to use regular expression in metadata search,  simply use the prefix _metareg:_ in the search string. 

To ensure metadata match when conducting multi-term search, one may use the following syntax at the main search bar: `join:term1,term2,term3,...,termN` and so on.  Doing so will ensure at least one of the terms can be found in the metadata for each search hit. Such syntax can be used to simulate search within metadata/tags.  Alternatively, fuzzy search can be conducted on metadata with syntax `related:term1,term2,term3,...,termN` and `similar:term1,term2,term3,...,termN`.

Simple contextual search can be achieved with the use of `in` or `scope` prefixes.  Say, to look up notes containing certain terms within notes with titles matching a certain substring. Simply do: `in:title_substring,term1,term2,...,termN`.  Likewise, to look up notes containing certain terms with metadata matching a certain substring, do `scope:metadata_substring,term1,term1,...,termN`.

To search for multiple terms, the easiest way is to use **Advanced Search**.  You can also specify boolean search queries with syntax like `and:term1,term2,term3,...,termN` to find notes containing all the terms (`or:term1,term2,term3,..,termN` to find notes containing one of the terms). 

**Custom Filters** The power of the above syntax lies in that it can also be included in preset search filters so that users can easily deploy.  Custom filters can be specified in [Settings](https://www.dropbox.com/s/cfve8rfp4yysro8/custom_filters.png?dl=0) delimited by semi-colons.  They are defaulted to be:

```
all;starred;A;B;C;D;E;F;G;H;I;J;K;L;M;N;O;P;Q;R;S;T;U;V;W;X;Y;Z
```

**all** is reserved for retrieving all notes, and **starred** reserved for retrieving starred notes. Single character filters are reserved for retrieving notes with titles beginning with said alphabets.

For searching within notes, **neutriNote** recognizes basic [Perl](https://remram44.github.io/regex-cheatsheet/regex.html) style patterns: `\d` for digits, `\s` for whitespace, etc.  

<a href="#toc">🔝 Back to top</a>
 

### <a name="advanced">Advanced Features</a>

### <a name="metadata">Metadata</a>
Metadata are general purpose text strings that exist outside note data.  They are searchable and can be used as tags.  To emulate filtering by tags, simply enter into the main search bar queries like `tag:term1,term2,term3,...,termN`, so that each term must be present in the metadata (in any order) for a note to be considered a match.  On the other hand, if the presence of any one term is sufficient for a note to be considered a match, use `tag*:term1,term2,term3,...,termN` instead.

<a href="#toc">🔝 Back to top</a>

### <a name="md">Markdown</a>
**neutriNote** supports [PHP Markdown Extra]( http://michelf.ca/projects/php-markdown/extra/) and LaTeX style mathematical expressions.  The easiest way to enter mathematical expressions is to wrap them in `$$`.  For inline math, use `\\(...\\)` as in the example below:
```
This expression \\(\sqrt{3x-1}+(1+x)^2\\) is an example of an inline equation.
```

To create in-document anchors/footnotes in PHP Markdown, use link syntax as in the following example:

```
# heading 1 {#header1}

## heading 2

* item 1:
    + sub item *1.1*
    + sub item *1.2*
* item 2
    + sub item *2.1*
    + sub item *2.2*
    + sub item 
    + [Link back to header 1](#header1)
```

To allow table of contents to be generated automatically, add a placeholder `<span id='toc' />`, tag each paragraph header with a unique ID by following the convention of PHP Markdown special attributes such as`{#id}`.  Try the example below:

```
Table of Contents
=================

<span id='toc' />

## Header 1 {#header1}
    * Your paragraph here...
    
## Header 2 {#header2}
    * Your paragraph here...
    
## Header 3 {#header3}
    * Your paragraph here...
```

To create link between notes, simply use one of the following syntax (`%20` denotes space):

```
[My File](file:///sdcard/neutriNote/my_file.txt)

[My File](./my_file.txt)

[My File](my_file.txt)

[GTD](get%20things%20done.txt)
```

Linking to an image under local repository, simply do:

```
![My Image](my_image.jpg)
```

Linking to notes from other apps that support hyperlinks, simply prefix note names with `http://neutriNote.io`.  For example:

```
https://neutriNote.io/my_diary

https://neutriNote.io/my_diary?search=first%20headquarter%20visit

```

Note that starting from Android 12, external linking must be enabled [manually](https://mastodon.social/@neutrinote/109666990309302664). 

(To navigate between notes, position your cursor anywhere in the link string then tap the `Web` icon from the toolbar.)

There is a conflict between Markdown italic symbol and LaTeX subscript symbol.  To workaround this problem, either escape the subscript symbols or wrap the expression in script block.  For example, instead of doing this:

`$$k_{n+1} = n^2 + k_n^2 - k_{n-1}$$`

do this:

`$$k\_{n+1} = n^2 + k\_n^2 - k\_{n-1}$$`

Or use script block with the desired type like this:
    
```
<script type="math/tex">k_{n+1} = n^2 + k_n^2 - k_{n-1}</script>
```

On the other hand, to allow line breaks within `$$` segments, use `\\\` instead of `\\`.

It's easy to customize the style of Markdown with popular inline CSS.  For more extensive styling needs, you can "swap out" built-in styling by declaring your CSS in  `~neutrinote_styles.txt`.  If your style is based off an existing Markdown theme, this process is pretty much effortless.  For example, to **solarize** your Markdown, simply copy and paste the following two lines into `~neutrinote_styles.txt`.

```
<link href="http://thomasf.github.io/solarized-css/solarized-light.min.css" rel="stylesheet"></link>
<script src="https://cdn.rawgit.com/google/code-prettify/master/loader/run_prettify.js"></script>
```

Power users may call `konsole.log()` to _inspect_ script snippets.  Note how the call is made in the sample script below:

```
<head>
    <script>
        const a = [3, 7, 8]
        const b = [9, 5, 6]
        let c = [...a, ...b].sort()
        konsole.log(c.toString())
    </script>
</head>
```

One may also directly tweak the built-in Markdown rendering engine by adding a note with the title `~neutrinote_head.txt`.  Additional styles and script snippets may go in there.  For example, to debug the rendering of Markdown elements, simply add:

```
<style>
    * {
        border: 2px solid red;
    }
</style>
```

Note that this method injects additional steps to the internal Markdown process and could lead to undesirable artifacts, its use should be limited in scope.  To disable, simply delete the note or renamed it to anything other than `~neutrinote_head.txt`.

<a href="#toc">🔝 Back to top</a>


### <a name="examples">Examples</a>
An example of how **neutriNote**'s rendering component could be used to plot a graph using [JSXGraph](http://jsxgraph.uni-bayreuth.de/wp/examples/):

```
<div id="box" class="box" style="width:500px; height:500px;"></div>
<head>
<script type='text/javascript' src='http://cdnjs.cloudflare.com/ajax/libs/jsxgraph/0.98/jsxgraphcore.js'></script>
<script type='text/javascript'>
 var b = JXG.JSXGraph.initBoard('box', {boundingbox: [-10, 10, 10, -10], axis:true});
b.create('functiongraph', [function(x){return Math.sin(x);},-Math.PI,2*Math.PI]);
</script>
</head>
```
An example of how **neutriNote**'s rendering component could be used to draw a simple shape:
    
```
<canvas id="example" width="200" height="200">
</canvas>

<head>
<script>
var example = document.getElementById('example');
var context = example.getContext('2d');
context.fillStyle = 'red';
context.fillRect(30, 30, 50, 50);
</script>  
</head>
```
Draw a simple diagram in plain text is easy using [yUML](http://yuml.me/diagram/scruffy/class/samples).  Try this (note the single ticks):
    
```
<img src="http://yuml.me/diagram/scruffy/usecase/[Cms Admin]^[User], [Customer]^[User], [Agent]^[User]" >

<img src="http://yuml.me/diagram/nofunky/class/`[Customer]->[Billing Address]`">
```

Tabular data can be processed by custom codes (note the placeholder cells for outputs):

```
| Type A | Type B | Type C |
|--------|:------:|-------:|
|       1|       2|       3|
|       2|       2|       4|
|       3|       2|       5|
|        |        |        |

<head>
    <script
        src="https://code.jquery.com/jquery-3.3.1.slim.min.js">
    </script>
    <script>
        $(document).ready(function()
        {
            $('table thead th').each(function(i)
            {
                sumCol(i);
            });
        });

        function sumCol(index)
        {
            var total = 0;
            $('table tr').each(function()
            {
                var value = parseInt($('td', this).eq(index).text());
                if (!isNaN(value))
                {
                    total += value;
                }
            });
            
            $('table tr:last td').eq(index).text('Total: ' + total);
        }
    </script>
</head>

```  

<a href="#toc">🔝 Back to top</a>


### <a name="automation">Automation</a>

**neutriNote** can easily be integrated into existing Tasker automation.  For example, to launch a third party Tasker plugin, it can be as simple as creating a Tasker profile to "observe" **Local Repository** events.  Specifically, to trigger third party sync plugins, simply add a blank file `~neutrinote_noop.txt` in **Local Repository** and have its modifications monitored by Tasker to piggyback a modification event corresponding to that file emitted by pull-to-refresh in **neutriNote**. 

One of the most useful features of Tasker is its rich set of variables.  One can easily maintain of log of the variables in **neutriNote** as well.  Consider this example of keeping clipboard history in **neutriNote**: simply create a profile to monitor the setting of Tasker's `%CLIP` variable, then add the following task (replace the path with that of your **Local Repository**):
    
```
A1: Variable Set [ Name:%NEWLINE To:Do Maths:Off Append:Off ] 
A2: Write File [ File:neutriNote/clipboard_events.txt Text:## %DATE %TIME %NEWLINE %CLIP %NEWLINE Append:On Add Newline:On ] If [ %clip neq %clip_prev ]
A3: Variable Set [ Name:%clip_prev To:%CLIP Do Maths:Off Append:Off ] 
```

Combined with other ways to extend **neutriNote**, there are essentially an infinite number of ways to automate the creation of richer note contents.

<a href="#toc">🔝 Back to top</a>


### <a name="textexpansion">Text Expansion</a>
**neutriNote** supports text expansion: simply highlight any shortcut word and tap the **Text Expansion** icon to expand the word.  All shortcuts are saved in a file called **~neutrinote_shortcuts**, with one definition per line in the format of `shortcut label|expanded text` (if you do not see the file, enable hidden files under **Settings**).  Below are some examples:  

```
cell|123-456-7890
email|john.smith@test.com

# Usage: select "highlight your_text" and expand, return "<mark>your_text</mark>".

highlight|<mark>???</mark>
```

Shortcuts can be defined for frequently used patterns for string replacements.  For example:

```
# Usage: select "encode some_text_string" and expand, some_text_string will be returned with all blank spaces encoded.

encode|neutriNote#replace \s %20
```

To replace all occurrences of a specific pattern by line breaks, simply:

```
# Usage: select "eol some_text_string" and expand, some_text_string will be returned with all blank spaces replaced by linebreaks.

eol|neutriNote#linebreak \s
```

To join multiple lines, try using this:

```
# Usage: select "join some_text_string" and expand, some_text_string will be returned with all newline characters replaced by blank spaces.

join|neutriNote#join
```

Or even this:

```
# Usage: select "concat some_text_string" and expand, some_text_string will be returned with all lines concatenated.

concat|neutriNote#remove \n
```

To glue multiple lines into one with symbols:

```
# Usage: select "glue some_text_string" and expand, some_text_string will be returned with all newline characters replaced by a bar between two blank spaces (with `<nano:sp>` denotes the space character). 

glue|neutriNote#join <nano:sp>|<nano:sp>
```

You can even split a string with the power of regex!  

```
# Usage: select `camel some_text_string` and expand, some_text_string will be split by camel case.

camel|neutriNote#split (?<!(^|[A-Z]))(?=[A-Z])|(?<!^)(?=[A-Z][a-z])

# Usage: select `snake some_text_string` and expand, some_text_string will be split by snake case.

snake|neutriNote#split _
```

`<nano:br>` can also be used as placeholders for linebreaks in shortcut definitions.  For example:

```
# Create a blank 3x2 table.

3x2|| | | |<nano:br>|---|---|---|---|<nano:br>| | | |<nano:br>|---|---|---|---|
```

An example to trim leading and trailing spaces from a body of text:

```
# Usage: select "trim some_text_string" and expand, leading and trailing spaces of some_text_string will be removed.

trim|neutriNote#trim
```

Shortcuts to obfuscate / defuscate a chunk of text:

```
# Usage: select "obfuscate some_text_string" and expand, some_text_string will be obfuscated.

obfuscate|neutriNote#encode

# Usage: select "defuscate some_text_string" and expand, some_text_string will be defuscated.

defuscate|neutriNote#decode
```

You can also use basic C style format specifiers to "morph" text snippets.

```
# Usage: select "addcomma some_numeric_string" and expand, some_numeric_string will be comma separated.

addcomma|neutriNote#morph ℅,d
```

With the helpers below, you can convert camel cases to / from snake cases with ease:

```
# Usage: select "s2c some_cool_string" and expand to obtain someCoolString.

s2c|neutriNote#snake2camel

# Usage: select "c2s someCoolString" and expand to obtain some_cool_string.

c2s|neutriNote#camel2snake
```

These simple shortcuts make it easy to sort lines:

```
# Usage: select "sort some_lines" and expand, some_lines will be sorted.

sort|neutriNote#sort

# Usage: select "rsort some_lines" and expand, some_lines will be sorted in reverse order.

rsort|neutriNote#rsort
```

There is even a way to remove HTML tags from strings:

```
# Usage: select "notag some_text_string" and expand to remove HTML tags from some_text_string.

notag|neutriNote#stripHTML
```

To remove zero-width spaces, simply do:

```
# Usage: select "zero some_text_string" and expand to remove zero-width spaces from some_text_string.

zero|neutriNote#nohiddenspace
```

You can create shortcuts for simple shell commands as well.  Give it a try by adding the prefix `neutriNote$` to the commands just like below:

```
date|neutriNote$ date
ps|neutriNote$ ps
```

To emulate the behavior of to-do list, shortcuts can be defined to mimic checkbox toggling.

```
# Usage: place cursor next to any asterisk and expand.  To toggle checkboxes, tap expand again.

*|[▪]
[▪]|[✔]
[✖]|[▪]
[✔]|[✖]
```

Multitasking especially with floating apps is easier with shortcut like this:

```
# Usage: launch a terminal without leaving neutriNote by expanding the shortcut.

termfloat|neutriNote#launch com.termux.window
```

Open a note directly from the current note with this:

```
# Usage: jump directly from one note to another by creating a "funnel."

hop|neutriNote#funnel
```

Quickly sift through the entire repo for a selected term:

```
# Usage: select "fetch some_text_string" and expand to look up some_text_string throughout the repo.

fetch|neutriNote#needle
```

Or issue canned searches like this:

```
# My favorite constant

fetch_pi|neutriNote#needle 3.141592653589793
```

The following shortcut allows you to create a link to the current note, at the position of the currently selected text:

```
# Usage: select "link some_text_string" and expand to create in clipboard a link to the current note at the position of the selected text.  A link from other notes to this note can then be created by pasting the current clipboard content into other notes.

link|neutriNote#createlink
```

The following shortcut allows Markdown comments to be created:

```
# Usage: select "comment some_comment_string" and expand to generate a Markdown comment.  Such comment will be bypassed by Markdown rendering.

comment|[???]::
```

(Since Markdown comments are hidden from rendering, they can alternatively be used for "watermarking" related notes in such a way that connections among notes will be manifested from searching for the watermarks.  Unlike metadata, watermarks are stored in notes and as a result can be located cross-platform.)

You can include basic parameters with the commands, just write them after the command shortcut and separate each parameter with space+commas like this: `shortcut_label param1 , param2 , param3`.  Select the whole string and tap the expand icon to paste the output.  Users of cURL can also simplify the definitons of their expansions with `neutriNote?` instead of `neutriNote$` and trail that directly by a URL.  Likewise use `neutriNote_json?` for URLs that expect JSON parameters.

<a href="#toc">🔝 Back to top</a>

### <a name="tagexpansion">Tag Expansion</a>
Tag Expansion is a streamlined way to input HTML/XML frictionlessly by cutting down on keystrokes significantly. On the surface, the syntax might resemble a lite version of [Emmet](https://docs.emmet.io/), but underneath the implementation is entirely different.  This feature is intended for better note-taking productivity rather than for application development.

To see it in action, first add the below shortcut to  **~neutrinote_shortcuts** (if you do not see the file, enable hidden files under **Settings**).  Also refer to the section above if you would want to learn more about [Text Expansion](#textexpansion).

```
# Usage: select "tagex some_tag_series_string".

tagex|neutriNote#tagExpand
```

Say you want to expand `div#banner>`, simply type: 
```
tagex div#banner>
```

Select the string in its entirety including `tagex` then tap **Text Expand**: 

```
<div id="banner">
</div>
```

Class names are supported as well:
```
tagex div#banner.intro>
```

After expansion: 
```

<div class="intro" id="banner">
</div>
```

Now add some text, either:
```
tagex div#banner.intro{Lorem Ipsum}>
```

Or:

```
tagex div#banner.intro>{Lorem Ipsum}>
```

Output:
```
<div class="intro" id="banner">Lorem Ipsum
</div>
```

Now the syntax for adding multiple items with the use of `*`:
```
tagex div#banner.intro>ul>li*3>
```

The expansion:
```
<div class="intro" id="banner">
    <ul>
        <li>
        </li>
        <li>
        </li>
        <li>
        </li>
    </ul>
</div>
```

Counters can be specified using `$`:
```
tagex div#banner.intro>ul>li.item$*3>
```

Output:
```

<div class="intro" id="banner">
    <ul>
        <li class="item1">
        </li>
        <li class="item2">
        </li>
        <li class="item3">
        </li>
    </ul>
</div>
```


Additional attributes can be specified like so:
```
tagex img[src="sky.jpg"][alt="Sunny day"]>
```

Output:
```
<img src="sky.jpg" alt="Sunny day">
</img>
```

Sibling tags can be specified using `+`:
```
tagex div.family>p.parent>span.sibling+span.sibling>
```

Output:
```

<div class="family">
    <p class="parent">
        <span class="sibling">
        </span>
        <span class="sibling">
        </span>
    </p>
</div>
```

"Climbing up" can be specified using `^`:
```
tagex div.family>p.parent>div>span.younger+span.younger^span.elder>
```

Output :
```

<div class="family">
    <p class="parent">
        <div>
            <span class="younger">
            </span>
            <span class="younger">
            </span>
        <span class="elder">
        </span>
        </div>
    </p>
</div>
```

<a href="#toc">🔝 Back to top</a>

### <a name="batchselect">Batch Select</a>
Special selection commands are available for better productivity.

* Tap `Top` icon in *Toolbox* when a section of text has been selected to extend selection all the way to the top, or if an anchor has been positioned above current cursor, extend selection up to the anchor.
* Tap `Bottom` icon in *Toolbox* when a section of text has been selected to extend selection all the way to the bottom, or if an anchor has been positioned below current cursor, extend selection down to the anchor.
* Place cursor to the right of either `(`, `{`, or `[` and tap `Bottom` icon to locate the closing counterpart.  Likewise to locate the opening counterpart, place cursor to the right of `)`, `}`, or `]` and tap `Top` .
* Tap **editor status** next to note title to gather statistics for current note when nothing is selected, or just the selected text when a section of text has been selected (experimental).
* To edit an ASCII drawing, select it and tap the **Sketch** icon.
* To encode/decode a portion of the note, select the portion and choose **Encode/Decode** from menu.
* Tap `(` or `)` from *Symbol Bar* when text selection is active to enclose the selected text in brackets.  Hint: also try out other symbol pairs.
* Edit multiple paragraphs: select multiple paragraphs and tap a symbol / action from  **Markdown Symbol Toolbar**.  For example, you can indent selected paragraphs by tapping `➡`, or turn selected paragraphs into a bulleted list simply by tapping `*`.
* Select the path of any linked image, tap **OCR** to extract text from the image.

<a href="#toc">🔝 Back to top</a>

    
### <a name="voicememo">Voice Memo</a>
**neutriNote** is compatible with Google Now dictation.  Simply say _Ok Google note to self_ and pick **neutriNote** to capture what you say.
 
<a href="#toc">🔝 Back to top</a>


### <a name="externalfonts">External Fonts</a>
It's easy to use external fonts such as those featured by Google Fonts in **neutriNote** (IMPORTANT: be sure to read their terms of use carefully):

1. Create a folder called `fonts` under your Local Repository, download and save the font file (.ttf) in that folder.  Note that external fonts will not be backup by **neutriNote**.
1. Enable hidden files under **Settings**.  Create a new note called `~neutrinote_fonts` if one does not exist yet.
1. Add a section in the note for the font (if there are multiple fonts, separate each section by a blank line) with a line dedicated to each of the following: 
    * Font name (any meaningful name)
    * Font file name (.ttf)
    * Link information (see instructions from Google Fonts)
    * CSS style (see instructions from Google Fonts)
1. The font is now ready for use in **neutriNote**.

For example, to use this [font](https://www.google.com/fonts#QuickUsePlace:quickUse/Family:Goudy+Bookletter+1911), just add this section to `~neutrinote_fonts`:
        
```
Goudy Bookletter 1911
GoudyBookletter1911.ttf
<link href='https://fonts.googleapis.com/css?family=Goudy+Bookletter+1911' rel='stylesheet' type='text/css'>
font-family: 'Goudy Bookletter 1911', serif;
```        

To skip the loading of a font, simply precede the first line of its entry with a `#`, as below using the example above:

```
# Goudy Bookletter 1911
GoudyBookletter1911.ttf
<link href='https://fonts.googleapis.com/css?family=Goudy+Bookletter+1911' rel='stylesheet' type='text/css'>
font-family: 'Goudy Bookletter 1911', serif;
```      

To use your device's default font, just add the below entry.  

```
System-Default
-
-
-
```

Please note this will only have effects on **neutriNote**'s editor screen, it has no effect on the app's Markdown rendering.


<a href="#toc">🔝 Back to top</a>

        
### <a name="ambientglow">Ambient Glow</a>
**Ambient Glow** is an experimental function that adjusts the color temperature of **neutriNote** to [approximate](https://en.wikipedia.org/wiki/Color_temperature#Categorizing_different_lighting) the level of your current environment for a more _atmospheric_ editing experience.  It differs from blue light filtering apps in that it does not demand your location information -- instead only light sensor data from Tasker will be used (to conserve battery).  [neutriNote Auto Theme](https://play.google.com/store/apps/details?id=com.appmindlab.autotheme) is required for this function to work properly.  Note that **Ambient Glow** will not be applied to Markdown and for users of blue light filters it is recommended that this function be disabled. 

<a href="#toc">🔝 Back to top</a>


### <a name="keyboard">Keyboard</a>
The following editor shortcuts are supported when connected to a physical keyboard:

| Shortcuts                  | Actions           |
| -------------------------- |:-----------------:|
| `Ctrl+S`                   | Save              |
| `Ctrl+F`                   | Local Find        | 
| `F3`                       | Find Next         | 
| `Ctrl+H`                   | Replace           | 
| `Ctrl+D`                   | Dictionary Lookup |
| `Ctrl+W`                   | Web Search        |
| `Ctrl+M`                   | Markdown          |
| `Ctrl+Z`                   | Undo              |  
| `Ctrl+Shift+Z`             | Redo              | 
| `Ctrl+]` or `Ctrl+I`       | Indent            |  
| `Ctrl+[` or `Ctrl+Shift+I` | Un-indent         | 
| `Ctrl++`                   | Zoom-in           |  
| `Ctrl+-`                   | Zoom-out          | 
| `Ctrl+Up`                  | Go to Top         |  
| `Ctrl+Down`                | Go to Bottom      |  
| `Ctrl+Left`                | Exit Mode         |  
| `Ctrl+Tab`                 | Expand Text       |  
| `Ctrl+=`                   | Calculate         | 


<a href="#toc">🔝 Back to top</a>


### <a name="gestures">Gestures</a>
Various user interface elements support gestures for better productivity:

* Note list screen:
    * Tap **list status** to navigate to the top of the list.
    * Long tap any blue rectangle to retrieve notes with related metadata.
    * Long tap any star to retrieve all starred notes.
    * Tap current sort method to reverse current sort order.
    * Swipe left/right on **list status** bar to navigate adjacent filters/days.
    * Double tap **list status** to resume default filter/day.
    * Long tap **list status** whenever update messages are shown to access the list of the recently updated items.

* Edit screen:
    * Tap **editor status** (to the right of the note title) to view note statistics and clipboard content; long tap clipboard content to view full clipboard content; long tap update status to view recent updates in other notes without leaving the current note.
    * Long tap the **Shortcut** icon to view user defined shortcuts.
    * Immediately after conducting a search, tap the **Search** icon to advance to the next match.
    * Double tap **editor status** to temporarily save the current cursor position.  
    * Swipe left on **editor status** to return to saved cursor position.
    * Swipe down **editor status** to launch in-note navigation.  Long press buttons to preview content at locations.
    * Swipe up **editor status** to access recently accessed notes (a.k.a **working set**).
    * After conducting search, swipe up/down **editor status** or long press `Top`/`Bottom` buttons to go to previous/next hits. 
    * For Android 6.0 or higher, swipe right on **editor status** will resume in edit screen the last scroll bar position from Markdown preview.

* Markdown preview:
    * (Experimental) For a more fluid e-book like reading experience, tap anywhere on a paragraph to reflow the text around screen after zooming. Tap any empty space to reflow the whole document (or swipe left on **editor status**). To resume the appearance of original text wrap, zoom all the way out and tap again.
    * Double tap **editor status** to temporarily save the current cursor position.  
    * Swipe left on **editor status** to return to saved cursor position.
    * Swipe down **editor status** to launch in-note search and navigation.
    * Swipe up **editor status** to access recently accessed notes (a.k.a **working set**).

<a href="#toc">🔝 Back to top</a>


### <a name="hacks">Hacks</a>
What follows are features that may conflict with the core functions of **neutriNote**.  Use at your own discretion.

You can tinker with the variables found inside of **~neutrinote_settings_data** (enabled by **Show Hidden** under **Settings**).  After saving your changes, do **Restore App Data** for the changes to take effect.  Note: altering the setting file could affect the stability of **neutriNote**.
    
| Variable Names                                    |  Values                                                                                                          |
| ------------------------------------------------- |:----------------------------------------------------------------------------------------------------------------:|
| com.appmindlab.nano.pref_append_custom_style      | `true`: **Extend** built-in styles with `~neutrinote_styles.txt`,  `false`: **Replace** built-in styles with `~neutrinote_styles.txt`                |
| com.appmindlab.nano.pref_auto_save_interval       | Specify the interval between auto save in seconds, which is only in effect when **Auto Save** is on.  Default: -1.  Note that periodic auto save will be disabled when the interval is set to be negative. |
| com.appmindlab.nano.pref_auto_toolbar_tag         | Specify a metadata substring pattern to enable auto show / hide toolbar (hint: tap screen to hide, double tap to re-display)                                         |
| com.appmindlab.nano.pref_canvas_strokes           | Fixed width symbols supported by sketch tool delimited by semicolons, e.g., `:;\;/;_;-;,;●` (vertical bar and semicolon not allowed) | 
| com.appmindlab.nano.pref_custom_date_format       | Override system date stamp format with custom [date format](https://developer.android.com/reference/android/icu/text/SimpleDateFormat.html) |
| com.appmindlab.nano.pref_custom_time_format       | Override system time stamp format with custom [time format](https://developer.android.com/reference/android/icu/text/SimpleDateFormat.html) |
| com.appmindlab.nano.pref_eval_built_in_variables  | `true`: evalute [built-in variables](#variables) in search or shortcut definitions            |  
| com.appmindlab.nano.pref_excluded_buttons         | Selectively hide toolbar buttons via a semicolon delimited string, e.g., `location;draw;replace` will hide the location, draw, and replace buttons on the toolbar.  The following buttons can be hidden: `markdown`, `time`, `date`, `location`, `expand`, `draw`, `top`, `bottom`, `find`, `replace`, `barcode`, `image`, `ocr`, `attach`, `define`, `calculate`, `search`, `encrypt`, `decrypt` |
| com.appmindlab.nano.pref_font_size_list           | Specify custom font size options delimited by semicolons.  Default: `8;10;12;14;16;18;24;32;48` |
| com.appmindlab.nano.pref_icon_behavior            | 0: animation off, 1: animation on, 2: [snooze](#snooze) animation                                                |
| com.appmindlab.nano.pref_indent_char              | Specify the character(s) to use for indentation.  Default: 4 spaces                                              |  
| com.appmindlab.nano.pref_keep_deleted_copies      | `true`: keep copies of deleted files under `trash_bin` folder                                                        |
| com.appmindlab.nano.pref_lab_mode                 | `true`: enable experimental features such as OCR, diff-tool                                                                |  
| com.appmindlab.nano.pref_launcher_tags             | Specify a search pattern for launcher shortcut icon.  Default is blank.  See [Launcher Shortcut](#launchershortcut). |  
| com.appmindlab.nano.pref_latex_single_dollar      | `true`: use single dollar signs to signify math expressions                                                      |
| com.appmindlab.nano.pref_linkify_trigger          | Specify a metadata substring pattern to open notes linkified by default                                          |
| com.appmindlab.nano.pref_local_priority_tag       | Specify a metadata substring pattern to prevent local copy from being overwritten by remote changes.  Note that conflicts may occur if a note is being edited on multiple devices |
| com.appmindlab.nano.pref_low_space_mode           | `true`: turn on [storage space saver](#storage) |   
| com.appmindlab.nano.pref_margin_list              | Specify custom margin options delimited by semicolons.  Default: `8;16;24` |
| com.appmindlab.nano.pref_markdown_trigger         | Specify a metadata substring pattern to open notes in Markdown by default                                        |
| com.appmindlab.nano.pref_max_backup_count         | Specify maximum number of backup copies to retain (pruning to occur during next backup).  Default: 10 |
| com.appmindlab.nano.pref_max_deleted_copies_age   | Specify maximum number of days deleted copies will be kept (pruning to occur during next backup).  Default: -1 (unlimited)      |
| com.appmindlab.nano.pref_max_sync_log_file_age    | Specify maximum number of days sync logs will be kept.  Default: 7 (1 week)      |
| com.appmindlab.nano.pref_max_sync_log_file_size   | Specify maximum size for each sync log file (factor of 200 KB).  Default: 2 (400 KB)      |
| com.appmindlab.nano.pref_new_note_file_type       | Specify file type for new notes.  Multiple type mode required (see below).  Default: `.txt`  | 
| com.appmindlab.nano.pref_new_note_title_template  | Specify title template for new notes.  Default: `New Note`  | 
| com.appmindlab.nano.pref_oled                     | `true`: dim screen elements for OLED screens               |
| com.appmindlab.nano.pref_open_in_markdown         | `true`: always open notes in markdown preview                                                                    |
| com.appmindlab.nano.pref_parse_python             | `true`: enable basic Python code interpretation.  Default: `false`   | 
| com.appmindlab.nano.pref_parse_mermaid            | `true`: enable Mermaid support.  Default: `false`   | 
| com.appmindlab.nano.pref_parse_typograms          | `true`: enable ASCII art to SVG support.  Default: `false`   | 
| com.appmindlab.nano.pref_parse_vue                | `true`: enable basic Vue.js components.  Default: `false`   | 
| com.appmindlab.nano.pref_preview_mode             | `start`: display the beginning of notes in preview, `end`: display the end, `off`: disable preview               |
| com.appmindlab.nano.pref_process_text_mode        | 0: disabled, 1: allow paste from other apps, 2: allow search from other apps .  Default: 0   | 
| com.appmindlab.nano.pref_remote_priority_tag      | Specify a metadata substring pattern to override local changes with remote changes when they occurred concurrently.  Note that conflicts may occur if a note is being edited on multiple devices |
| com.appmindlab.nano.pref_safe_mode_tag            | Specify a metadata substring pattern to disable internal Markdown parser                                         |
| com.appmindlab.nano.pref_show_toolbar             | `true`: always show edit toolbar (hint: tap screen to hide, double tap to re-display)                                                                                 |
| com.appmindlab.nano.pref_star_at_top              | `true`: place starred notes above other notes in list view.  Default: `false`          |
| com.appmindlab.nano.pref_toolbox_mode             | `stateful`: keep editor toolbox scroll position (default), `stateless`: always reset editor toolbox scroll position, `pin_save`: keep save button visible            |
| com.appmindlab.nano.pref_working_set_size         | Specify size of working set (the set of recently accessed notes).  Default: 6          |
             
Advanced users may enable multiple text file types for **neutriNote**.  To setup, please carefully follow all the steps below:

1. Backup ALL app settings and notes.
1. Add a blank file called `~neutrinote_multitype.txt` to your **Local Repository**.
1. Un-install **neutriNote** (or clear the app's data under Android's system settings).
1. Re-install **neutriNote**.
1. Once rescan finishes, file extensions will appear in note titles.
1. Restore app data.

(To reverse the support of multiple file types, you would need to remove the file `~neutrinote_multitype.txt`, then un-install/re-install **neutriNote**.)

> To enable search history transfer across devices, simply add a note called `~neutrinote_search_history.txt`.   Search history can then be cloned when app data are restored by tapping **Restore App Data** on your other devices.

Note that **neutriNote Connector** will not handle files without `.txt` extension.  To sync files without `.txt` extension with Dropbox you would have to install a third party app or install [**neutriNote Connector+**](https://play.google.com/store/apps/details?id=com.appmindlab.connectorplus).  (If you have **neutriNote Connector** installed, you would need to remove it prior to launching **neutriNote Connector+**.  If you have **neutriNote Connector+** installed, you would need to _re-install_ the app.)

<a href="#toc">🔝 Back to top</a>


### <a name="builtinvariables">Built-in Variables</a>
Built-in variables may be used in search or shortcut definitions.  For example, to find notes with tomorrow's time stamp, simply type `@tomorrow` in the search box.  You can even include built-in variables in **Custom Filters**, say, for listing notes containing tomorrow's time stamp, or include them in shortcut definitions to generate text expansion snippets on the fly.

| Variables            | Descriptions                            |                              
| ---------------------|-----------------------------------------|
| @title               | Title of the current note.              |
| @created             | Created time of the current note.       |                     
| @modified            | Last modified time of the current note. |
| @accessed            | Last accessed time of the current note. |
| @clipboard           | Clipboard content.                      |
| @location            | Current location (experimental).        |
| @yesterday           | Yesterday's date stamp.                 |
| @today               | Today's date stamp.                     |
| @tomorrow            | Tomorrow's date stamp.                  |
| @now                 | Current time stamp.                     |

See [Hacks](#hacks) for information on how to enable the use of built-in variables.

<a href="#toc">🔝 Back to top</a>


### <a name="customvariables">Custom Variables (v3.3.0 or above)</a>

Custom variables are variables with the prefix `@@` and are used as shortcuts in conducting local search.  Say you have a shortcut defined like this:

```
# End of Paragraph
eop|\\n\\n
```

Enter `@@eop` in local search bar and tap search will take you to the boundary of each paragraph.  (Indeed a rudimentary tool to overview long notes when combined with gestures.)

Note that only shortcuts defined for simple string replacement are supported.

<a href="#toc">🔝 Back to top</a>


### <a name="storage">Storage Saver</a>
For devices equipped with SD cards, it is possible to store backups on SD cards to save space in internal storage. 

1. Tap **Backup App Data**.
1. Add `com.appmindlab.nano.pref_low_space_mode|true` to **~neutrinote_settings_data**.
1. Tap **Restore App Data**.
1. Future backups will be stored at `/Android/data/com.appmindlab.nano/files/neutrinote_export` under the SD card.

Notice that the backups will be automatically removed to reclaim storage space if neutriNote is uninstalled.

<a href="#toc">🔝 Back to top</a>


### <a name="api">API</a>
neutriNote's Markdown engine is fully modular and swappable.  If you are familar with compiler scripting and would like to integrate your own parser, you would need to use the following entry points in your code:

| Methods              | Descriptions           |                              
| ---------------------|----------------------|
| init(document)       | Initialize the framework. |
| getData()            | Get raw content from a note.  |                     
| prepare()            | Prepare for the rendering process. |
| setContent(html)     | Set view to rendering outcome.   |

Adopt this pattern of invoking neurtiNote in your script:

```
(function (){
  ////////////
  // Set up //
  ////////////
  neutriNote.init(document);

  //////////////////
  // Get raw data //
  //////////////////
  var str = neutriNote.getData();

  ///////////////////////////
  // Prepare for rendering //
  ///////////////////////////
  neutriNote.prepare();

  ///////////
  // Parse //
  ///////////
  
  ... <- Custom conversion logic goes here!

  /////////////////
  // Set content //
  /////////////////
  neutriNote.setContent(str)

})(window, document);
```


To illustrate, suppose you simply want to render everything in italics, all you need is to create `~neutrinote_script.txt` and paste in the following code:

```
(function (){
  ////////////
  // Set up //
  ////////////
  neutriNote.init(document);

  //////////////////
  // Get raw data //
  //////////////////
  var str = neutriNote.getData();

  ///////////////////////////
  // Prepare for rendering //
  ///////////////////////////
  neutriNote.prepare();

  ///////////
  // Parse //
  ///////////
  str = '<i>' + str + '</i>';

  /////////////////
  // Set content //
  /////////////////
  neutriNote.setContent(str)

})(window, document);
```

Now go to your note and tap render to view the output of your custom parser.

More useful parsing can be achieved by following the same pattern.  Take a look at this example of integrating [org-mode](https://raw.githubusercontent.com/appml/nano/master/samples/%7Eneutrinote_script.txt) into neutriNote.

To restore default PHP Markdown syntax, just remove `~neutrinote_script.txt`.

<a href="#toc">🔝 Back to top</a>


### <a name="python">Python Support (Experimental)</a>
**neutriNote** can evaluate in-note Python code snippets.  To enable this feature, simply set Python parsing flag to `true` as shown under [Hacks](#hacks) section.  

To see it in action, copy the code below and tap **Markdown Preview** button:

```
<script type="text/python">
    from browser import document
    document <= "Hello world !"
</script>
```

A slightly more complex example:

```
<script type="text/python">
    from browser import document

    # Sort a list
    aList = [5, 8, 7, 6, 2, 3]
    aList = sorted(aList)
    result = '\n'.join(str(i) for i in aList)

    # Print the output
    document <= result
</script>
```

(Note that the `script` tag is required to indicate the scope of Python code.)

<a href="#toc">🔝 Back to top</a>

### <a name="javascript">In-note JavaScript (Experimental)</a>

**neutriNote**'s JavaScript mode provides a lightweight, renderless, <a href="https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop">REPL</a> environment for executing simple JavaScript in-note. Those who are familiar with Juptyer Notebook's interactive mode should recognize some of the similarities found in this in-note interpreter.  Furthermore, those custom logic can in turn be re-used to extend **neutriNote**'s built-in editor functionalities.  The following examples provide a glimpse of its potential in action.

Firstly, to make one-off JavaScript call, simply create a <a href="#textexpansion">shortcut</a> like this (note: feel free to pick any shortcut name for all examples in this section):

```
# Usage: select "evaljs js_function_call" and expand.
evaljs|neutriNote#interactivejs
```

E.g., to determine the square root of 144, simply type `evaljs Math.sqrt(144)`, select the string just entered, and tap the **Text Expand** button.

For quick prototyping, one may create a shortcut like this:

```
# Usage: select "protojs js_function_call" and expand.
protojs|neutriNote#snippetjs
```

Suppose now you want to try out the following snippet:

```
function substr(str, start, end)
{
    return str.substring(start, end);
}
substr("dog, cat, fish", 5, 8)  
```

For a quick preview of whether the code works as expected, type `protojs` before the code block, select the shortcut name including the entire code block, and tap the **Text Expand** button.  (Notice that the code block ends with a function call after the declaration of the function.)

Frequently used short functions can be included right within shortcut definitions to reduce typings.  For example:

```
# Usage: select "presetjs extract(my_string, starting_position, ending_position)" and expand.
presetjs|neutriNote#inlinejs function extract(str, start, end) { return str.substring(start, end); }
```

To invoke the function with parameters, for example to extract the first three characters from `apple`, simply enter and select `presetjs extract("apple", 0, 2)`, then tap the **Text Expand** button.

One can also build collections of functions and store them in dedicated notes.  Suppose you have a note called `my_toolbox.js` containing a series of function declarations:

```
function myfunc1(param1, param2) {
    ...
}

function myfunc2(param1, param2, param3) {
    ...
}

function myfunc2(param1, param2, param3) {
    ...
}

```

When you create a shortcut referring to the note `my_toolbox.js` as below, you can invoke any functions defined in the "library" in-note!

```
# Usage: select "storedjs func(param1, param2, ...)" and expand, assuming func() is defined in the named note.
storedjs|neutriNote#filejs my_toolbox.js
```

In this case, you can call upon any function included in `my_toolbox.js`.  For example, to invoke `myfunc1` declared in `my_toolbox.js`, simply by enter in `storedjs myfunc1(...)`, select the string, then tap the **Text Expand** button.

<a href="#toc">🔝 Back to top</a>

### <a name="components">Web Components</a>
**neutriNote** supports reusable user defined components through Vue.js.  This is especially useful for including frequently used note elements. 

To enable, simply enable Vue parsing shown under [Hacks](#hacks) section and create a new note with the title `app.js` and **neutriNote** will handle the rest.

To see it in action, copy the following to `app.js`, the file where all component declarations are to be placed: 

```
Vue.createApp({
    data() {
        return {
            message: 'Hello Vue!'
        }
    }
}).mount('#app')
``` 

That's it!  Now see how easy it is to deploy a component anywhere throughout your notes as long as it is inside a `div` block by the id `app`.

```
<div id="app">{{ message }}</div>
```

Note that currently **neutriNote** does not support the import of external components, so not a substitute for any full-scale development architecture.

<a href="#toc">🔝 Back to top</a>


### <a name="diagrams">Diagrams</a>

[Mermaid](https://mermaid-js.github.io/mermaid/) provides a Markdown like syntax for making graphs.  To enable its use, simply add this line to **~neutrinote_setting_data** followed by **Restore App Data**.  For more details, see the [Hacks](#hacks) section.

```
com.appmindlab.nano.pref_parse_mermaid|true
```

Some snippets to show how easy it is to specify inline drawings.

```
<pre class="mermaid">
    flowchart TD 
    A-->B
</pre>

<pre class="mermaid">
    graph TD
    A-->B
    A-->C
    B-->D
    C-->D
</pre>
```

To expedite the workflow further, consider adding this shortcut to your collection.

```
# Usage: select "mermaid your_mermaid_graph" and expand, your_mermaid_graph will be properly wrapped for rendering.

mermaid|<pre class="mermaid"><nano:br>???<nano:br></pre>
```

See [here](#textexpansion) for more information on how to get started with using **Text Expansion**.

Alternatively, existing drawings can also be turned into [SVG diagrams](https://github.com/google/typograms/). Firstly, add the following line to **~neutrinote_setting_data** then tap **Restore App Data**.

```
com.appmindlab.nano.pref_parse_typograms|true
```

To avoid excessive typings, consider adding this shortcut to your collection.
```
# Usage: select "typo your_ascii_drawing" and expand, your_ascii_drawing will be properly wrapped for rendering.

typo|<div style="background:white"><nano:br><script type="text/typogram"><nano:br>???<nano:br></script><nano:br></div>
```

Now you are ready to apply the shortcut to any ASCII drawings and have their SVG versions rendered in Markdown view.


<a href="#toc">🔝 Back to top</a>


### <a name="texteditor">Text Editor</a>
Though outside the scope of note taking, **neutriNote** can be used as a lightweight text editor to supplement apps such as Dropbox or Google Drive across all folders.  Changes committed will be sent back to original locations of edited files instead of storing in **Local Repository**, if the files are located outside **Local Repository**.  (Note that files not stored in **Local Repository** will not be cataloged by **neutriNote**'s search engine.)

<a href="#toc">🔝 Back to top</a>


### <a name="editorless">Editorless Read/Write</a>

**neutriNote** provides a variety of ways to quickly add new contents to notes bypassing the opening of the notes.  This is especially useful for working with long notes on devices with limited memory.  To name a few of these methods:  

* To paste into multiple notes simultaneously: at the main note list, long press and select a set of notes, then tap **Append Clipboard** from the top menu to paste clipboard content into the set of selected notes.

* To paste content into another note without leaving the editor screen, follow these steps: 
    1. Apply the swipe up gesture on the top right status. The **working set** note picker will appear at the bottom.  
    1. At the note picker, scroll all the way to the right and tap **Pick a note**.  
    1. Specify a target note and tap **Paste** to append clipboard content to the target without leaving the current note.

* (Experimental, v3.9.9 or above) Should there be a need for "side-note" like writing during **Markdown Preview**, one may do so by adding a note titled `neutriNote Scrapbook.txt`.  An input box will appear in the notification area and all text entered through it will go directly to the **scrapbook**.  [Built-in Variables](#builtinvariables) may be used in the input box to ease text entry in the limited space. 

* When using the **Working Set** feature as described in [gestures](#gestures) section, long press any of the menu items will reveal the latest changes of the selected item without opening the note.  

<a href="#toc">🔝 Back to top</a>


### <a name="snooze">Snooze (Experimental)</a>
With **neutriNote**'s non-intrusive visual reminders, it is easy to set aside notes for editing later, or build a habit of reviewing saved notes.  Simply enable snooze animation by appending the following to `~neutrinote_settings_data`:

```
com.appmindlab.nano.pref_icon_behavior|2
``` 

Then add special **snooze strings** such as `+1h` ("snooze for an hour") or `+2d` ("snooze for two days") to the metadata of selected notes.  By doing so a non-intrusive animation will remind you to view the notes if they have not been visited long enough.  The visual reminders would be dismissed as soon as the notes were opened.  To de-activate the snooze, simply remove the snooze string from the note's metadata.  


| Units              |  Examples                          |
|--------------------|:----------------------------------:|
| `m` for minutes    | `+30m`: snooze for 30 minutes      |
| `h` for hours      | `+8h`: snooze for 8 hours          |
| `d` for days       | `+3d`: snooze for 3 days           |
| `w` for weeks      | `+2w`: snooze for 2 weeks          |
| `M` for months     | `+3M`: snooze for a quarter        |
| `y` for years      | `+10y`: snooze for a decade        |

To transfer snooze to another device, be sure to tap **Backup/Restore App Data**.  Even more useful is that snooze strings are also fully searchable, they work just like regular metadata!

<a href="#toc">🔝 Back to top</a>

### <a name="launchershortcuts">Launcher Shortcuts (Experimental)</a>

With **Launcher Shortcuts**, you can add a launcher icon for any [custom search filter](#search).  

Say there is a need to pull up notes with metadata containing the word `news`.  Simply do the followings:

1. Tap **Backup App Data**.
1. Add to `~neutrinote_settings_data` this string: `com.appmindlab.nano.pref_launcher_tags|meta:news`.
1. Tap **Restore App Data**.
1. Now long press the icon of **neutriNote** on your launcher.  `meta:news` will appear as one of the shortcut options.  Now drag and drop the shortcut over to anywhere in your launcher to create an icon.
1. Tap the newly created icon to jump directly to the list of notes with metadata matching the search term `news`.

While not recommended as each launcher app imposes its own upper limit on the number of app shortcuts, multiple shortcuts can be defined by joining filter strings with semicolons.  For example, the following represents a one-line declaration of multiple launcher shortcuts.

```
com.appmindlab.nano.pref_launcher_tags|meta:drawings;titlereg:Python*;org:@today,@tomorrow
```

<a href="#toc">🔝 Back to top</a>


### <a name="misc">Miscellaneous</a>
**neutriNote** comes with many goodies for capturing text based data without switching away such as the built-in barcode scanner.  Another is a handy calculator for solving mathematical expressions based on [Math.js](http://mathjs.org/docs/expressions/syntax.html) (network connection required).  To see how that works, try one of the following examples in your notes:

1. Select the expression. 
1. Tap the calculator button from the toolbar.
1. View the answer with the option to paste it back into your note.

    
```
sin(45 deg) ^ 2

cos(45 deg)

5.08 cm to inch

det([-1, 2; 3, 1])

log(10000, 10)
```

<a href="#toc">🔝 Back to top</a>

        
### <a name="performance">Performance</a>
When editing a long note, hide the title bar to reduce lags.  

In general, using default font style can help reduce the time in opening long notes.

For users who do not use mathematics expressions, mathematics rendering can be disabled by entering a `https://` under **Mathematics** in **Settings**. Markdown rendering should be faster with mathematics disabled.

<a href="#toc">🔝 Back to top</a>


### <a name="log">Log Tool</a>
**neutriNote** provides a simple log mechanism to monitor **Local Repository** changes caused externally.  This is useful especially when cross-platform sync is in use.  To activate logging, simply add a file called `~neutrinote_sync.log` under **Local Repository** and observe that the `log` folder will be created automatically to record remote data changes such as inserts, deletes, or in-place updates.  Log attributes such as sizes and recycle frequencies can be customized further via `pref_max_sync_log_file_age` and `pref_max_sync_log_file_size` settings (see [Hacks](#hacks) section).  

Note that logging may have impacts on overall performance and battery consumption.  To stop recording changes, simply delete `~neutrinote_sync.log`. 

<a href="#toc">🔝 Back to top</a>


### <a name="encryption">Encryption (v3.3.9 or above)</a>
Encryption support in **neutriNote** is provided via **[OpenKeyChain](https://play.google.com/store/apps/details?id=org.sufficientlysecure.keychain)** which is an open source, independently audited tool.  This setup allows your encryption keys to be stored independent of **neutriNote**.

Assuming **OpenKeyChain** has been installed, simply follow these steps to encrypt note content: 

1. Select a section of note that you want encrypted.
1. Tap the **Encrypt** button 🔒 under the editor toolbar to launch **OpenKeyChain**.
1. Once in **OpenKeyChain**, either pick an existing key or use a password to encrypt.
1. Close **OpenKeyChain** and you will be sent back to the note.
1. Paste the newly encrypted content in to replace the text selected.

Follow these steps to decrypt a note:
                                          
1. To decrypt, tap anywhere within `-----BEGIN PGP MESSAGE-----` and `-----END PGP MESSAGE-----`.
1. Tap the **Decrypt** button 🔓 under the editor toolbar to launch **OpenKeyChain**.                                       
1. Once in **OpenKeyChain**, your content will automatically be decrypted.
1. Pick **Copy to clipboard** at the menu.
1. Close **OpenKeyChain** and you will be sent back to the note.
1. Paste the newly decrypted content in to replace the text selected. 

<a href="#toc">🔝 Back to top</a>


### <a name="ocr">OCR</a>
OCR is disabled by default.  To enable OCR in [neutriNote](https://play.google.com/store/apps/details?id=com.appmindlab.nano) installed from **Google Play**, simply follow the instructions under [Hacks](#hacks) and set `com.appmindlab.nano.pref_lab_mode` to true.  Once done, OCR icon will appear in the tool bar.  To enable OCR in [neutriNote CE](https://f-droid.org/en/packages/com.appmindlab.nano/) installed from **F-Droid**, simply install [OCR with Tesseract 4](https://f-droid.org/en/packages/io.github.subhamtyagi.ocr) from **F-Droid**.

<a href="#toc">🔝 Back to top</a>


### <a name="relocate">Relocate Local Repository</a>
While generally not recommended, there may come a time when **Local Repository** has to be relocated.  Please handle the following steps with care:

1. Backup ALL app settings and notes.
1. For pre-Android 9 devices, copy **Local Repository** folder to its new location.  For Android 9 or above, **Local Repository** can only be located anywhere under `/Android/data/com.appmindlab.nano/files`.
1. Un-install **neutriNote** (or clear the app's data under Android's system settings).
1. Re-install **neutriNote**.
1. Point **Local Repository** to its new location.
1. Restore app data.

<a href="#toc">🔝 Back to top</a>


### <a name="issues">Known Issues</a>
Anytime a note is accessed from widget, if there is a note already being edited, the note originally being edited will exit without saving.  **neutriNote** does not distinguish between opening a note from widget or from the note list, the currently opened note will be closed to make way for the newly opened note.  It is thus highly recommended that important changes be saved right away.

If a note needs to be renamed, do so within **neutriNote**.  Certain cloud sync would also change the case of note titles.  **neutriNote** would detect those changes and be case insensitive accordingly.  However, **neutriNote** would not delete notes unless their titles match exactly.  Therefore it is so crucial that notes be renamed from the end of **neutriNote**.

To improve app stability in lower-end devices, **neutriNote** supports note size up to 1.5 MB.  Notes beyond the size will automatically be moved to a folder called `import_errors`.  To bring them back into **neutriNote**, you would need to split the notes into files below 1.5 MB and move them into the repository folder.

<a href="#toc">🔝 Back to top</a>


### <a name="faq">FAQs</a>
**No folder support?** **neutriNote** is designed to provide a flat, hierarchy-free, ["low cognitive load"](http://blog.codinghorror.com/trees-treeviews-and-ui/) note taking experience so that the number of taps can be minimized, folder navigation would require a nested UI and more taps to get to notes beyond the root level.  On top of that, offline search would need to traverse levels of folders in such a way that turnaround time could vary perceivably.  Metadata used together with custom filters provides more general organization than folders (a note can match multiple metadata simultaneously).

**Story behind the name?** [This](https://en.wikipedia.org/wiki/Neutrino) came up when trying to conjure up something that conveys unclutterness. 

<a href="#toc">🔝 Back to top</a>


### <a name="privacy">Privacy Policy</a>
This app does not gather personal information. Location data can always be disabled via Settings.  A menu option is also provided to clear search history.

<a href="#toc">🔝 Back to top</a>


### <a name="todo">TODO</a>
Keep the app as crash-proof as possible.

<a href="#toc">🔝 Back to top</a>


### <a name="source">Source Code</a>
For further customization, **neutriNote**'s source code is available on [GitHub](https://github.com/appml/neutrinote) as **Community Edition**.

<a href="#toc">🔝 Back to top</a>


### <a name="about">About</a>
Every effort has been made to ensure that all third-party software used be properly acknowledged (see license information in the **About** dialog).  Please feel free to contact by [email](mailto:lightandshadowscamera@gmail.com) anytime should such information be found incomplete or inaccurate.

You can also visit [Product Page](https://mastodon.social/@neutrinote) for development updates regarding the app.

To further support neutriNote's development, please visit developer's [Ko-fi](https://ko-fi.com/neutriNote) page.

<a href="#toc">🔝 Back to top</a>

<div style="display:flex" >
    <a href="https://play.google.com/store/apps/details?id=com.appmindlab.nano">
        <img src="https://play.google.com/intl/en_us/badges/images/generic/en_badge_web_generic.png"
             alt="Get it on Google Play" 
             height="64" />
    </a>
    <a href="https://f-droid.org/packages/com.appmindlab.nano">
        <img src="https://fdroid.gitlab.io/artwork/badge/get-it-on.png"
             alt="Get it on F-Droid"
             height="64">
    </a>
</div>

