### neutriNote User Guide

1. [Getting Started](#started)
1. [Backup and Restore](#backup)
1. [Search Tools](#search)
1. [Advanced Features](#advanced)
    * [Metadata](#metadata)
    * [Markdown](#md)
    * [Automation](#automation)
    * [Text Expansion](#textexpansion)
    * [Voice Memo](#voicememo)
    * [External Fonts](#externalfonts)
    * [Ambient Glow](#ambientglow)
    * [Hacks](#hacks)
    * [Misc.](#misc)
    * [Examples](#examples) 
1. [Performance](#performance)
1. [Known Issues](#issues)
1. [FAQs](#faq)
1. [Privacy Policy](#privacy)
1. [TODO](#todo)
1. [About](#about)

#### <a name="started">Getting Started</a>
Thank you for choosing **neutriNote**.  

Right after installation, be sure to follow the onscreen instruction and choose a location for **Local Repository**.  

If your repository is empty, you may add notes right away.  

If you have installed **neutriNote** previously, you may pick the repository already on your device.  

If you have settings backed up from your previous installation, you may also choose [Restore App Data](https://www.dropbox.com/s/nveejx2dn1pdbqi/navigation_drawer.png?dl=0, "Backup/Restore App Data") to restore settings.

To enable sync is easy, either install a third party app like [Syncthing](https://play.google.com/store/apps/details?id=com.nutomic.syncthingandroid&hl=en) and register your repository with it or get [Dropbox Connector](https://play.google.com/store/apps/details?id=com.appmindlab.connector) -- a Dropbox adapter designed just for 
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

Search can also be limited to metadata by using the prefix _meta:_ in the search string.  A search string such as _meta:personal_ will return all notes with the substring _personal_ in the metadata.  It is also possible to use [regular expression](http://en.m.wikipedia.org/wiki/Glob_(programming)) in metadata search,  simply use the prefix _metareg:_ in the search string. 

To ensure metadata match when conducting multi-term search, one may use the following syntax at the main search bar: `join:term1,term2,term3` and so on.  Doing so will ensure at least one of the terms can be found in the metadata for each search hit. Such syntax can be used to simulate search within metadata/tags.

To search for multiple terms, the easiest way is to use **Advanced Search**.  You can also specify boolean search queries with syntax like `and:term1,term2,term3,...,termN` to find notes containing all the terms (`or:term1,term2,term3,..,termN_` to find notes containing one of the terms). 

**Custom Filters** The power of the above syntax lies in that it can also be included in preset search filters so that users can easily deploy.  Custom filters can be specified in [Settings](https://www.dropbox.com/s/cfve8rfp4yysro8/custom_filters.png?dl=0) delimited by semi-colons.  They are defaulted to be:

```
all;starred;A;B;C;D;E;F;G;H;I;J;K;L;M;N;O;P;Q;R;S;T;U;V;W;X;Y;Z
```

**all** is reserved for retrieving all notes, and **starred** reserved for retrieving starred notes. Single character filters are reserved for retrieving notes with titles beginning with said alphabets.


#### <a name="advanced">Advanced Features</a>

* <a name="metadata">_Metadata_</a>
    * Metadata are general purpose text strings that exist outside note data.  They are searchable and can be used as tags.
        
* <a name="md">_Markdown_</a>
   * **neutriNote** supports [PHP Markdown Extra]( http://michelf.ca/projects/php-markdown/extra/) and LaTeX style mathematical expressions.  The easiest way to enter mathematical expressions is to wrap them in `$$`.  For inline math, use `\\(...\\)` as in the example below:
```
This expression \\(\sqrt{3x-1}+(1+x)^2\\) is an example of an inline equation.
```
    * Note: `$$` is used to avoid conflicts with the dollar sign.  If `$` is preferred for your mathematical expressions, simply append the code below to your note:
```
<script type="text/x-mathjax-config"> 
MathJax.Hub.Config({ tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]} }); 
</script>
```

* To create in-document anchors/footnotes in PHP Markdown, use link syntax as in the following example:

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

* To allow table of contents to be generated automatically, add a placeholder `<span id='toc' />`, tag each paragraph header with a unique ID by following the convention of PHP Markdown special attributes such as`{#id}`.  Try the example below:

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

* To create link between notes, simply use one of the following syntax (`%20` denotes space):

```
[My File](file:///sdcard/neutriNote/my_file.txt)

[My File](./my_file.txt)

[My File](my_file.txt)

[GTD](get%20things%20done.txt)
```

* Linking to an image under local repository, simply do:

```
![My Image](my_image.jpg)
```

* There is a conflict between Markdown italic symbol and LaTeX subscript symbol.  To workaround this problem, either escape the subscript symbols or wrap the expression in script block.  For example, instead of doing this:

    `$$k_{n+1} = n^2 + k_n^2 - k_{n-1}$$`

    do this:
    
    `$$k\_{n+1} = n^2 + k\_n^2 - k\_{n-1}$$`

    Or use script block with the desired type like this:
    
```
<script type="math/tex">k_{n+1} = n^2 + k_n^2 - k_{n-1}</script>
```
    
* <a name="examples">_Examples_</a>

    * An example of how **neutriNote**'s rendering component could be used to plot a graph using [JSXGraph](http://jsxgraph.uni-bayreuth.de/wp/examples/):

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

* An example of how **neutriNote**'s rendering component could be used to draw a simple shape:
    
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

* Draw a simple diagram in plain text is easy using [yUML](http://yuml.me/diagram/scruffy/class/samples).  Try this (note the single ticks):
    
```
<img src="http://yuml.me/diagram/scruffy/usecase/[Cms Admin]^[User], [Customer]^[User], [Agent]^[User]" >

<img src="http://yuml.me/diagram/nofunky/class/`[Customer]->[Billing Address]`">
```

* <a name="automation">_Automation_</a>

    * **neutriNote** can be easily automated using Tasker.  For example, **neutriNote**'s theme can be set according to light level with the use of ([neutriNote Auto Theme](https://play.google.com/store/apps/details?id=com.appmindlab.autotheme)) with these steps:
        1. Create a _new_ task in Tasker.
        1. Add a _new_ action, choose **App** from **Select Action Category**.
        1. Choose the extension just downloaded from the app selection screen. 
        1. Now the task is created and ready for use in any of your profiles.  For example, create a new profile that will be triggered when the display is on (add a new profile, then choose **State** -> pick **Display**) to launch the task.  Now each time the screen is turned on, **neutriNote** will automatically select a theme based on the current light level.
    * Steps above apply to [neutriNote Backup+](https://play.google.com/store/apps/details?id=com.appmindlab.backupplus) as well.
    * For users who are interested in keeping clipboard history, simply create a profile to monitor the setting of Tasker's `%CLIP` variable, then add the following task (replace the path with that of your **Local Repository**):
    
```
A1: Variable Set [ Name:%NEWLINE To:Do Maths:Off Append:Off ] 
A2: Write File [ File:neutriNote/clipboard_events.txt Text:## %DATE %TIME %NEWLINE %CLIP %NEWLINE Append:On Add Newline:On ] If [ %clip neq %clip_prev ]
A3: Variable Set [ Name:%clip_prev To:%CLIP Do Maths:Off Append:Off ] 
```

* <a name="textexpansion">_Text Expansion_</a>

    * **neutriNote** supports text expansion: simply highlight any shortcut word and tap the **Text Expansion** icon to expand the word.  All shortcuts are saved in a file called **~neutrinote_shortcuts**, with one definition per line in the format of `shortcut label|expanded text` (if you do not see the file, enable hidden files under **Settings**).  Below are some examples:  

```
cell|123-456-7890
email|john.smith@test.com

# Usage: select "highlight your_text" and expand, return "<mark>your_text</mark>"
highlight|<mark>???</mark>
```

   * **Experimental:** You can create shortcuts for simple shell commands as well.  Give it a try by adding the prefix `neutriNote$` to the commands just like below:

```
date|neutriNote$ date
ps|neutriNote$ ps
```

* You can include basic parameters with the commands, just write them after the command shortcut and separate each parameter with space+commas like this: `shortcut_label param1 , param2 , param3`.  Select the whole string and tap the expand icon to paste the output.  Users of cURL can also simplify the definitons of their expansions with `neutriNote?` instead of `neutriNote$` and trail that directly by a URL.

    
* <a name="voicememo">_Voice Memo_</a>

   * **neutriNote** is compatible with Google Now dictation.  Simply say _Ok Google note to self_ and pick **neutriNote** to capture what you say.
 
* <a name="externalfonts">_External Fonts_</a>
    * It's easy to use external fonts such as those featured by Google Fonts in **neutriNote** (IMPORTANT: be sure to read their terms of use carefully):
        1. Create a folder called `fonts` under your Local Repository, download and save the font file (.ttf) in that folder.  Note that external fonts will not be backup by **neutriNote**.
        1. Enable hidden files under **Settings**.  Create a new note called `~neutrinote_fonts` if one does not exist yet.
        1. Add a section in the note for the font (if there are multiple fonts, separate each section by a blank line) with a line dedicated to each of the following: 
            * Font name (any meaningful name)
            * Font file name (.ttf)
            * Link information (see instructions from Google Fonts)
            * CSS style (see instructions from Google Fonts)
        1. The font is now ready for use in **neutriNote**.
        1. For example, to use this [font](https://www.google.com/fonts#QuickUsePlace:quickUse/Family:Goudy+Bookletter+1911), just add this section to `~neutrinote_fonts`:
        
```
Goudy Bookletter 1911
GoudyBookletter1911.ttf
<link href='https://fonts.googleapis.com/css?family=Goudy+Bookletter+1911' rel='stylesheet' type='text/css'>
font-family: 'Goudy Bookletter 1911', serif;
```        
        
* <a name="ambientglow">_Ambient Glow_</a>

    * **Ambient Glow** is an experimental function that adjusts the color temperature of **neutriNote** to [approximate](https://en.wikipedia.org/wiki/Color_temperature#Categorizing_different_lighting) the level of your current environment for a more _atmospheric_ editing experience.  It differs from blue light filtering apps in that it does not demand your location information -- instead only light sensor data from Tasker will be used (to conserve battery).  [neutriNote Auto Theme](https://play.google.com/store/apps/details?id=com.appmindlab.autotheme) is required for this function to work properly.  Note that **Ambient Glow** will not be applied to Markdown and for users of blue light filters it is recommended that this function be disabled. 
    
* <a name="hacks">_Hacks_</a>

    * You may also tinker with the variables found inside of **~neutrinote_settings_data** (enabled by **Show Hidden** under **Settings**).  After saving your changes, do **Restore App Data** for the changes to take effect.  Note: altering the setting file could render **neutriNote** unstable.
    
| Variable Names                             |  Values                                   |
| ------------------------------------------ |:-----------------------------------------:|
| com.appmindlab.nano.pref_open_in_markdown  | Set true to always open notes in markdown preview |
| com.appmindlab.nano.pref_show_toolbar      | Set true to always show edit toolbar | 
| com.appmindlab.nano.pref_latex_single_dollar | Set true to use single dollar signs to signify math expressions |  

    
* <a name="misc">_Miscellaneous_</a>

    * **neutriNote** comes with many goodies for capturing text based data without switching away such as the built-in barcode scanner.  Another is a handy calculator for solving mathematical expressions based on [Math.js](http://mathjs.org/docs/expressions/syntax.html) (network connection required).  To see how that works, try one of the following examples in your notes:
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
        
#### <a name="performance">Performance</a>
Tips: When editing a long note, hide the title bar to reduce lags.

#### <a name="issues">Known Issues</a>
Anytime a note is accessed from widget, if there is a note already being edited, the note originally being edited will exit without saving.  **neutriNote** does not distinguish between opening a note from widget or from the note list, the currently opened note will be closed to make way for the newly opened note.   It is thus highly recommended that important changes be saved right away.

#### <a name="faq">FAQs</a>
**No folder support?  Why?** First off, this app is designed for note taking with the least number of taps, folder navigation would require a nested UI and more taps to get to notes not at the root level.  Furthermore, offline search would need to traverse levels of folders and turn around time could vary perceivably.  Metadata used together with custom filters provides more general organization than folders (a note can match multiple metadata simultaneously).

#### <a name="privacy">Privacy Policy</a>
This app does not gather personal information. Location data can always be disabled via Settings.  A menu option is also provided to clear search history.

#### <a name="todo">TODO</a>
Keep the app as crash-proof as possible.

#### <a name="about">About</a>
Every effort has been made to ensure that all third-party software used be properly acknowledged (see license information in the **About** dialog).  Please feel free to contact [me](mailto:lightandshadowscamera@gmail.com) anytime should such information be found incomplete or inaccurate.

You can also visit [Product Page](https://plus.google.com/u/0/communities/117565395761503074053) for development updates regarding the app.
