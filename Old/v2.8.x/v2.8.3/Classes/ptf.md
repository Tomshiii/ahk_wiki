This script contains a stew of classes and group declarations to make file and name management throughout my scripts easier and more consistent.

***
# <u>class ptf {</u>
`Point to File`, this class contains all directory and file locations that I can possibly assign. Keeping all definitions in the one place allows for easier adjusting of file locations in the future, as well as an easier time for another user to come through and adjust.

#### `ptf.Variable`
<u>Example #1</u>
```autohotkey
;for directory locations
ptf.SupportFiles ;passes: A_WorkingDir "\Support Files"
```

#### `ptf["variable"]`
<u>Example #1</u>
```autohotkey
;for absolute file locations
ptf["settings"] ;passes: A_MyDocuments "\tomshi\settings.ini"
```
***

# <u>class browser {</u>
This class contains a set of objects to define browser `winTitles` & `classes`. Currently contains information for; firefox, chrome, msedge & vscode

<u>Example #1</u>
```autohotkey
;for winTitle
broswer.firefox.winTitle ;passes: ahk_exe firefox.exe

;for class
browser.firefox.class ;passes: ahk_class MozillaWindowClass
```
***

# <u>class Editors {</u>
This class contains a set of objects to define Editor `winTitles` & `classes`. Currently contains information for; Adobe Premiere Pro, Adobe After Effects, Adobe Photoshop & Davinci Resolve

<u>Example #1</u>
```autohotkey
;for winTitle
editor.Premiere.winTitle ;passes: ahk_exe Adobe Premiere Pro.exe

;for class
editor.Premiere.class ;passes: ahk_class Premiere Pro
```
***

## <u>GroupAdd</u>
The script then goes on to define a browser group, and an editor group.
***