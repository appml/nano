## User Guide 

<sup>[[Japanese Edition](https://github.com/ayatakesi/neutriNote/blob/master/index.md)]</sup>

1. [Getting Started](#started)
1. [Backup and Restore](#backup)
1. [Search Tools](#search)
1. [Advanced Features](#advanced)
    * [Metadata](#metadata)
    * [Markdown](#md)
    * [Automation](#automation)
    * [Text Expansion](#textexpansion)
    * [Batch Select](#batchselect)
    * [Voice Memo](#voicememo)
    * [External Fonts](#externalfonts)
    * [Ambient Glow](#ambientglow)
    * [Keyboard](#keyboard)
    * [Gestures](#gestures)
    * [Hacks](#hacks)
    * [Built-in Variables](#variables)
    * [Storage Saver](#storage)
    * [API](#api)
    * [Snooze](#snooze)
    * [Misc.](#misc)
    * [Examples](#examples) 
1. [Performance](#performance)
1. [Known Issues](#issues)
1. [FAQs](#faq)
1. [Privacy Policy](#privacy)
1. [TODO](#todo)
1. [About](#about)

### <a name="started">Getting Started</a>
Thank you for choosing **neutriNote**.  

Right after installation, be sure to follow the onscreen instruction and choose a location for **Local Repository**.  

If your repository is empty, you may add notes right away.  

If you have installed **neutriNote** previously, you may pick the repository already on your device.  

If you have settings backed up from your previous installation, you may also choose [Restore App Data](https://www.dropbox.com/s/nveejx2dn1pdbqi/navigation_drawer.png?dl=0, "Backup/Restore App Data") to restore settings.

To enable sync is easy, either install a third party app like [Syncthing](https://play.google.com/store/apps/details?id=com.nutomic.syncthingandroid&hl=en) and register your repository with it or get [neutriNote Connector](https://play.google.com/store/apps/details?id=com.appmindlab.connector) -- a Dropbox adapter designed just for 
**neutriNote**.  

Even without add-ons, **neutriNote** is ready for use.  Explore around to discover many features that would make **neutriNote** a highly integrated part of your note taking experience (for example, long tap metadata label to retrieve notes sharing [similar](https://www.dropbox.com/s/tqa3h774xrn49zd/metadata_long_click.png?dl=0) label and tap the local find icon in the edit screen to jump to the next match).  To extend it into a tool for personal information management, please do take a moment to go over the following sections.  New users may also want to check out [Backup and Restore](#backup) for ways to preserve note data beyond the sync mechanism.

**IMPORTANT**: from v1.3.1, **neutriNote** supports **Runtime Permissions** in Android Marshmallow devices.  Be sure to grant **neutriNote** permission to access external storage for its **Local Repository** to work properly.  To enable previously denied permissions, go to **neutriNote**'s **App Info** under Android, renable the permissions and restart the app.

#### <a name="backup">Backup and Restore</a>
If you have already activated **Local Repository**, your notes will be sync seamlessly to the repository.  You can replicate your notes remotely by sharing the folder with third party apps such as [Syncthing](https://play.google.com/store/apps/details?id=com.nutomic.syncthingandroid&hl=en).  **IMPORTANT**: Do NOT use stale repositories since they could be out of sync.  Always use the method described in the [Getting Started](#started) section from above to initialize and assign repositories.
    
**Incremental Backup** is another way to copy your notes in non-intrusive fashion. To enable, simply do so from Settings.  Then your notes and app settings will be backed up incrementally at least once daily to a internal storage folder called _neutrinote_export_.  Note: exported app settings data are stored in regular notes with prefix _.neutrinote_ so that they can be sync no differently from other notes.

For more demanding scenarios, check out [neutriNote Backup+](https://play.google.com/store/apps/details?id=com.appmindlab.backupplus).

#### <a name="search">Search Tools</a>
While notes can be retrieved based on modified time, accessed time, and location as providied by the user interface, **neutriNote** supports high precision text based search and [regular expression](http://en.m.wikipedia.org/wiki/Glob_(programming)).  The syntax below are also highly reusable when they are included as part of the preset filters (under Settings).

**Search by Fields** It is possible to restrict search to a specified field.  For example, at the main search bar over the note list, search can be limited to titles by using the prefix `title:` in the search string.  A search string like`title:log` will return all notes with the substring `log` in the titles.

Search can also be limited to metadata by using the prefix _meta:_ in the search string.  A search string such as _meta:personal_ will return all notes with the substring _personal_ in the metadata (likewise _meta:_ will return notes without metadata). It is also possible to use [regular expression](http://en.m.wikipedia.org/wiki/Glob_(programming)) in metadata search,  simply use the prefix _metareg:_ in the search string. 

To ensure metadata match when conducting multi-term search, one may use the following syntax at the main search bar: `join:term1,term2,term3` and so on.  Doing so will ensure at least one of the terms can be found in the metadata for each search hit. Such syntax can be used to simulate search within metadata/tags.

To search for multiple terms, the easiest way is to use **Advanced Search**.  You can also specify boolean search queries with syntax like `and:term1,term2,term3,...,termN` to find notes containing all the terms (`or:term1,term2,term3,..,termN` to find notes containing one of the terms). 

**Custom Filters** The power of the above syntax lies in that it can also be included in preset search filters so that users can easily deploy.  Custom filters can be specified in [Settings](https://www.dropbox.com/s/cfve8rfp4yysro8/custom_filters.png?dl=0) delimited by semi-colons.  They are defaulted to be:

```
all;starred;A;B;C;D;E;F;G;H;I;J;K;L;M;N;O;P;Q;R;S;T;U;V;W;X;Y;Z
```

**all** is reserved for retrieving all notes, and **starred** reserved for retrieving starred notes. Single character filters are reserved for retrieving notes with titles beginning with said alphabets.

For searching within notes, **neutriNote** recognizes basic [Perl](http://www.erudil.com/preqr.pdf) style patterns: `\d` for digits, `\s` for whitespace, etc.  
 

### <a name="advanced">Advanced Features</a>

### <a name="metadata">Metadata</a>
Metadata are general purpose text strings that exist outside note data.  They are searchable and can be used as tags.
        
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
http://neutriNote.io/my_diary

http://neutriNote.io/my_diary?search=first%20headquarter%20visit

```

* There is a conflict between Markdown italic symbol and LaTeX subscript symbol.  To workaround this problem, either escape the subscript symbols or wrap the expression in script block.  For example, instead of doing this:

    `$$k_{n+1} = n^2 + k_n^2 - k_{n-1}$$`

    do this:
    
    `$$k\_{n+1} = n^2 + k\_n^2 - k\_{n-1}$$`

    Or use script block with the desired type like this:
    
```
<script type="math/tex">k_{n+1} = n^2 + k_n^2 - k_{n-1}</script>
```

It's easy to customize the style of Markdown with popular inline CSS.  For more extensive styling needs, you can "swap out" built-in styling by declaring your CSS in  `~neutrinote_styles.txt`.  If your style is based off an existing Markdown theme, this process is pretty much effortless.  For example, to **solarize** your Markdown, simply copy and paste the following two lines into `~neutrinote_styles.txt`.

```
<link href="http://thomasf.github.io/solarized-css/solarized-light.min.css" rel="stylesheet"></link>
<script src="https://cdn.rawgit.com/google/code-prettify/master/loader/run_prettify.js"></script>
```
    
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

### <a name="automation">Automation</a>

**neutriNote** can be easily automated using Tasker.  For example, **neutriNote**'s theme can be set according to light level with the use of ([neutriNote Auto Theme](https://play.google.com/store/apps/details?id=com.appmindlab.autotheme)) with these steps:

1. Create a _new_ task in Tasker.
1. Add a _new_ action, choose **App** from **Select Action Category**.
1. Choose the extension just downloaded from the app selection screen. 
1. Now the task is created and ready for use in any of your profiles.  For example, create a new profile that will be triggered when the display is on (add a new profile, then choose **State** -> pick **Display**) to launch the task.  Now each time the screen is turned on, **neutriNote** will automatically select a theme based on the current light level.

Steps above apply to [neutriNote Backup+](https://play.google.com/store/apps/details?id=com.appmindlab.backupplus) as well.

The following illustrates finer control over expiring automated backups.  Backups kept over 180 days will be purged automatically or chronologically once the number of backups exceeds 30 copies.

```
A1: Send Intent
[Action:com.appmindlab.nano.ACTION_FULL_BACKUP 
Cat:None 
Mime Type: 
Data: 
Extra:com.appmindlab.nano.EXTRA_MAX_BACKUP_COUNT:30 
Extra:com.appmindlab.nano.EXTRA_MAX_BACKUP_AGE:180 
Extra: 
Package: 
Class: 
Target:Broadcast Receiver ] 
```

For users who are interested in keeping clipboard history, simply create a profile to monitor the setting of Tasker's `%CLIP` variable, then add the following task (replace the path with that of your **Local Repository**):
    
```
A1: Variable Set [ Name:%NEWLINE To:Do Maths:Off Append:Off ] 
A2: Write File [ File:neutriNote/clipboard_events.txt Text:## %DATE %TIME %NEWLINE %CLIP %NEWLINE Append:On Add Newline:On ] If [ %clip neq %clip_prev ]
A3: Variable Set [ Name:%clip_prev To:%CLIP Do Maths:Off Append:Off ] 
```

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
notag|neutriNote#removeHTML
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

You can include basic parameters with the commands, just write them after the command shortcut and separate each parameter with space+commas like this: `shortcut_label param1 , param2 , param3`.  Select the whole string and tap the expand icon to paste the output.  Users of cURL can also simplify the definitons of their expansions with `neutriNote?` instead of `neutriNote$` and trail that directly by a URL.


### <a name="batchselect">Batch Select</a>
Special selection commands are available for better productivity.

* Tap `Top` icon in *Toolbox* when a section of text has been selected to extend selection all the way to the top, or if an anchor has been positioned above current cursor, extend selection up to the anchor.
* Tap `Bottom` icon in *Toolbox* when a section of text has been selected to extend selection all the way to the bottom, or if an anchor has been positioned below current cursor, extend selection down to the anchor.
* Tap **editor status** next to note title to gather statistics for current note when nothing is selected, or just the selected text when a section of text has been selected (experimental).
* To edit an ASCII drawing, select it and tap the **Sketch** icon.
* To encode/decode a portion of the note, select the portion and choose **Encode/Decode** from menu.
* Tap `(` or `)` from *Symbol Bar* when text selection is active to enclose the selected text in brackets.  Hint: also try out other symbol pairs.
* Edit multiple paragraphs: select multiple paragraphs and tap a symbol / action from  **Markdown Symbol Toolbar**.  For example, you can indent selected paragraphs by tapping `➡`, or turn selected paragraphs into a bulleted list simply by tapping `*`.
* Select the path of any linked image, tap **OCR** to extract text from the image.

    
### <a name="voicememo">Voice Memo</a>
**neutriNote** is compatible with Google Now dictation.  Simply say _Ok Google note to self_ and pick **neutriNote** to capture what you say.
 

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

        
### <a name="ambientglow">Ambient Glow</a>
**Ambient Glow** is an experimental function that adjusts the color temperature of **neutriNote** to [approximate](https://en.wikipedia.org/wiki/Color_temperature#Categorizing_different_lighting) the level of your current environment for a more _atmospheric_ editing experience.  It differs from blue light filtering apps in that it does not demand your location information -- instead only light sensor data from Tasker will be used (to conserve battery).  [neutriNote Auto Theme](https://play.google.com/store/apps/details?id=com.appmindlab.autotheme) is required for this function to work properly.  Note that **Ambient Glow** will not be applied to Markdown and for users of blue light filters it is recommended that this function be disabled. 

### <a name="keyboard">Keyboard</a>
The following editor shortcuts are supported when connected to a physical keyboard:

| Shortcuts                  | Actions           |
| -------------------------- |:-----------------:|
| `Ctrl-S`                   | Save              |
| `Ctrl-F`                   | Local Find        | 
| `F3`                       | Find Next         | 
| `Ctrl-H`                   | Replace           | 
| `Ctrl-D`                   | Dictionary Lookup |
| `Ctrl-W`                   | Web Search        |
| `Ctrl-Z`                   | Undo              |  
| `Ctrl-Shift-Z`             | Redo              | 
| `Ctrl-]` or `Ctrl-I`       | Indent            |  
| `Ctrl-[` or `Ctrl-Shift-I` | Un-indent         | 


### <a name="gestures">Gestures</a>
Various user interface elements support gestures for better productivity:

* Note list screen:
    * Tap **list status** to navigate to the top of the list.
    * Long tap any blue rectangle to retrieve notes with related metadata.
    * Long tap any star to retrieve all starred notes.
    * Tap current sort method to reverse current sort order.
    * Swipe left/right on **list status** bar to navigate adjacent filters/days.
    * Double tap **list status** to resume default filter/day.

* Edit screen:
    * Tap **editor status** (to the right of the note title) to view note statistics and clipboard content; long tap clipboard content to view full clipboard content; long tap update status to view recent updates in other notes without leaving the current note.
    * Long tap the **Shortcut** icon to view user defined shortcuts.
    * Immediately after conducting a search, tap the **Search** icon to advance to the next match.
    * Double tap **editor status** to temporarily save the current cursor position.  
    * Swipe left on **editor status** to return to saved cursor position.
    * After conducting search, dial up/down **editor status** to go to previous/next hits.
    * For Android 6.0 or higher, swipe right on **editor status** will resume in edit screen the last scroll bar position from Markdown preview.

### <a name="hacks">Hacks</a>
What follows are features that may conflict with the core functions of **neutriNote**.  Use at your own discretion.

You can tinker with the variables found inside of **~neutrinote_settings_data** (enabled by **Show Hidden** under **Settings**).  After saving your changes, do **Restore App Data** for the changes to take effect.  Note: altering the setting file could affect the stability of **neutriNote**.
    
| Variable Names                                    |  Values                                                                                                          |
| ------------------------------------------------- |:----------------------------------------------------------------------------------------------------------------:|
| com.appmindlab.nano.pref_open_in_markdown         | `true`: always open notes in markdown preview                                                                    |
| com.appmindlab.nano.pref_markdown_trigger         | Specify a metadata substring pattern to open notes in Markdown by default                                        |
| com.appmindlab.nano.pref_safe_mode_tag            | Specify a metadata substring pattern to disable internal Markdown parser                                         |
| com.appmindlab.nano.pref_linkify_trigger          | Specify a metadata substring pattern to open notes linkified by default                                          |
| com.appmindlab.nano.pref_latex_single_dollar      | `true`: use single dollar signs to signify math expressions                                                      |
| com.appmindlab.nano.pref_indent_char              | Specify the character(s) to use for indentation.  Default: 4 spaces                                              |  
| com.appmindlab.nano.pref_append_custom_style    | `true`: **Extend** built-in styles with `~neutrinote_styles.txt`.  `false`: **Replace** built-in styles with `~neutrinote_styles.txt`.                |
| com.appmindlab.nano.pref_show_toolbar             | `true`: always show edit toolbar                                                                                 |
| com.appmindlab.nano.pref_canvas_strokes           | Fixed width symbols supported by sketch tool delimited by semicolons, e.g., `:;\;/;_;-;,;●` (vertical bar and semicolon not allowed) | 
| com.appmindlab.nano.pref_font_size_list           | Specify custom font size options delimited by semicolons.  Default: `8;10;12;14;16;18;24;32;48` |
| com.appmindlab.nano.pref_margin_list              | Specify custom margin options delimited by semicolons.  Default: `8;16;24` |
| com.appmindlab.nano.pref_excluded_buttons         | Selectively hide toolbar buttons via a semicolon delimited string, e.g., `location;draw;replace` will hide the location, draw, and replace buttons on the toolbar.  The following buttons can be hidden: `markdown`, `time`, `date`, `location`, `expand`, `draw`, `top`, `bottom`, `find`, `replace`, `barcode`, `image`, `ocr`, `define`, `calculate`, `search` |
|com.appmindlab.nano.pref_custom_date_format        | Override system date stamp format with custom [date format](https://developer.android.com/reference/android/icu/text/SimpleDateFormat.html) |
|com.appmindlab.nano.pref_custom_time_format        | Override system time stamp format with custom [time format](https://developer.android.com/reference/android/icu/text/SimpleDateFormat.html) |
| com.appmindlab.nano.pref_preview_mode             | `start`: display the beginning of notes in preview, `end`: display the end, `off`: disable preview               |
| com.appmindlab.nano.pref_icon_behavior            | 0: animation off, 1: animation on, 2: [snooze](#snooze) animation                                                |
| com.appmindlab.nano.pref_keep_deleted_copies      | `true`: keep copies of deleted files under `trash_bin` folder                                                        |
| com.appmindlab.nano.pref_max_deleted_copies_age   | Specify maximum number of days deleted copies will be kept (pruning to occur during next backup).  Default: -1 (unlimited)      |
| com.appmindlab.nano.pref_local_priority_tag       | Specify a metadata substring pattern to prevent local copy from being overwritten by remote changes.  Note that conflicts may occur if a note is being edited on multiple devices |
| com.appmindlab.nano.pref_eval_built_in_variables  | `true`: evalute [built-in variables](#variables) in search or shortcut definitions            |  
| com.appmindlab.nano.pref_low_space_mode           | `true`: turn on [storage space saver](#storage) |   
             
Advanced users may enable multiple text file types for **neutriNote**.  To setup, please carefully follow all the steps below:

1. Backup ALL app settings and notes.
1. Add a blank file called `~neutrinote_multitype.txt` to your **Local Repository**.
1. Un-install **neutriNote** (or clear the app's data under Android's system settings).
1. Re-install **neutriNote**.
1. Once rescan finishes, file extensions will appear in note titles.
1. Restore app data.

(To reverse the support of multiple file types, you would need to remove the file `~neutrinote_multitype.txt`, then un-install/re-install **neutriNote**.)

Note that **neutriNote Connector** will not handle files without `.txt` extension.  To sync files without `.txt` extension with Dropbox you would have to install a third party app or install [**neutriNote Connector+**](https://play.google.com/store/apps/details?id=com.appmindlab.connectorplus).  (If you have **neutriNote Connector** installed, you would need to remove it prior to launching **neutriNote Connector+**.)

### <a name="variables">Built-in Variables (v2.3.4) </a>
Built-in variables may be used in search or shortcut definitions.  For example, to find notes with tomorrow's time stamp, simply type `@tomorrow` in the search box.  You can even include built-in variables in **Custom Filters**, say, for listing notes containing tomorrow's time stamp, or include them in shortcut definitions to generate text expansion snippets on the fly.

| Variables            | Descriptions                            |                              
| ---------------------|-----------------------------------------|
| @title               | Title of the current note.              |
| @created             | Created time of the current note.       |                     
| @modified            | Last modified time of the current note. |
| @accessed            | Last accessed time of the current note. |
| @clipboard           | Clipboard content.                      |
| @yesterday           | Yesterday's date stamp.                 |
| @today               | Today's date stamp.                     |
| @tomorrow            | Tomorrow's date stamp.                  |
| @now                 | Current time stamp.                     |

See [Hacks](#hacks) for information on how to enable the use of built-in variables.

### <a name="storage">Storage Saver</a>
For devices equipped with SD cards, it is possible to store backups on SD cards to save space in internal storage. 

1. Tap **Backup App Data**.
1. Add `com.appmindlab.nano.pref_low_space_mode|true` to **~neutrinote_settings_data**.
1. Tap **Restore App Data**.
1. Future backups will be stored at `/Android/data/com.appmindlab.nano/files/neutrinote_export` under the SD card.

Notice that the backups will be automatically removed to reclaim storage space if neutriNote is uninstalled.

### <a name="api">API (v2.0.8) </a>
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
        
### <a name="performance">Performance</a>
When editing a long note, hide the title bar to reduce lags.  

In general, using default font style can help reduce the time in opening long notes.

For users who do not use mathematics expressions, mathematics rendering can be disabled by entering a `.` under **Mathematics** in **Settings**. Markdown rendering should be faster with mathematics disabled.

### <a name="issues">Known Issues</a>
Anytime a note is accessed from widget, if there is a note already being edited, the note originally being edited will exit without saving.  **neutriNote** does not distinguish between opening a note from widget or from the note list, the currently opened note will be closed to make way for the newly opened note.   It is thus highly recommended that important changes be saved right away.

If a note needs to be renamed, do so within **neutriNote**.  Certain cloud sync would also change the case of note titles.  **neutriNote** would detect those changes and be case insensitive accordingly.  However, **neutriNote** would not delete notes unless their titles match exactly.  Therefore it is so crucial that notes be renamed from the end of **neutriNote**.

To improve app stability in lower-end devices, **neutriNote** supports note size up to 1.5 MB.  Notes beyond the size will automatically be moved to a folder called `import_errors`.  To bring them back into **neutriNote**, you would need to split the notes into files below 1.5 MB and move them into the repository folder.

### <a name="faq">FAQs</a>
**No folder support?** **neutriNote** is designed to provide a flat, hierarchy-free, ["low cognitive load"](http://blog.codinghorror.com/trees-treeviews-and-ui/) note taking experience so that the number of taps can be minimized, folder navigation would require a nested UI and more taps to get to notes beyond the root level.  On top of that, offline search would need to traverse levels of folders in such a way that turnaround time could vary perceivably.  Metadata used together with custom filters provides more general organization than folders (a note can match multiple metadata simultaneously).

**Story behind the name?** [This](https://en.wikipedia.org/wiki/Neutrino) came up when trying to conjure up something that conveys unclutterness. 

### <a name="privacy">Privacy Policy</a>
This app does not gather personal information. Location data can always be disabled via Settings.  A menu option is also provided to clear search history.

### <a name="todo">TODO</a>
Keep the app as crash-proof as possible.

### <a name="about">About</a>
Every effort has been made to ensure that all third-party software used be properly acknowledged (see license information in the **About** dialog).  Please feel free to contact by [email](mailto:lightandshadowscamera@gmail.com) anytime should such information be found incomplete or inaccurate.

You can also visit [Product Page](https://plus.google.com/u/0/communities/117565395761503074053) for development updates regarding the app.

To further support neutriNote's development, please visit developer's [Ko-fi](https://ko-fi.com/neutriNote) page.
