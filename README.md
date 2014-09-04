subl-handler
============

## What is this?

This vbs script handles `subl:` url scheme to open it in your text editor.

Example link
``` subl://open?url=file://C%3A%5Chtdocs%5Cmyapp%5Cvendor%5Claravel%5Cframework%5Csrc%5CIlluminate%5CSupport%5CFacades%5CFacade.php&line=214 ```

I found it very useful when debugging Laravel based applications because Laravel's exception page use subl links on every filename.
Of course it works only on local webserver (in your local filesystem).

## Compatibility

There are two versions of this script:
- `sublime.vbs` - this script works fine with **sublime** or any other text editor that supports line numbers attached to the end of filename (filename:line_number)
- `eclipse.vbs` - this script works fine with **eclipse** or any other text editor that **doesn't** support line numbers on the end of filename

If the "sublime" version doesn't work fine for you, use "eclipse" version which works fine even with notepad.exe :)

## Installation

- select the script version you need according to "compatibility" section of this readme
- copy the selected script to any location on your disk. I suggest to copy it to c: or c:\Users or something like this. The file will have to stay there because it will handle subl: links and follow it to your text editor
- run the script and follow instructions on the screen

## Usage

Click on and subl: link to see it working.
*Note for Mozilla Firefox users*: Firefox will ask you what to do with subl: links for the first time you click on it. Simply click the OK button and Firefox will choose the default action, which is this script since you installed it. Firefox will ask about this only once.

## How it works / Is it safe?

It is safe to run this script, it doesn't change any files in your system only add some small entry into windows registry.

When you run this script without parameters it will run itself ad administrator to be able to import .reg file into windows registry.
The imported .reg file looks like this:
```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\subl]
@="URL:subl Protocol"
"URL Protocol"=""

[HKEY_CLASSES_ROOT\subl\shell]

[HKEY_CLASSES_ROOT\subl\shell\open]

[HKEY_CLASSES_ROOT\subl\shell\open\command]
@="\"wscript.exe\" \"C:\\sublime.vbs\" \"C:\\Program Files\\Sublime Text 3\\sublime_text.exe\" %1"
```

It adds this script as a handler for subl: protocol.

When you click subl: link your browser run this scrip which reads the subl: link, parse it and run the selected text editor.
