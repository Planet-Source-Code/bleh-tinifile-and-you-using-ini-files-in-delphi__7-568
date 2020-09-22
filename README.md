<div align="center">

## TINIFile And You \- Using INI Files in Delphi


</div>

### Description

Learn the magic of the TINIFile object.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[bleh](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/bleh.md)
**Level**          |Beginner
**User Rating**    |4.6 (106 globes from 23 users)
**Compatibility**  |Delphi 5, Delphi 4
**Category**       |[Files/ File Controls/ Input/ Output](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/files-file-controls-input-output__7-3.md)
**World**          |[Delphi](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/delphi.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/bleh-tinifile-and-you-using-ini-files-in-delphi__7-568/archive/master.zip)





### Source Code

<font face="Verdana" size="2">
<div align="center"><b>TINIFile And You - Using INI Files in Delphi</b></div>
<p>This article is just a simple explanation of how to implement
the TINIFile object into your Delphi application. Thankfully, the
wonderful people at Borland have created this object for us,
so we don't have to actually write out the API to do so (such
as in VB). If you already understand what an INI File is and how it works,
you can skip directly to Part 2. Otherwise, I suggest you read Part 1 first</p>
<b>Part 1: Understanding INI Files</b>
<p>INI Files are nothing more than text files that
are used by many programs to store application and operating
system values, such as a programs window position, colors, or virtually
any other settings. INI Files were rather abundant in Windows 3.1, and
to alleviate this growing problem, Microsoft decided that with Windows
95, it would implement a database they so lovingly called the registry (there
is a good tutorial on here for the Windows Registry in Delphi, so I won't
bother getting into it here). Despite this fact, INI Files are still very
much in use within the Windows operating system. A good example is the
win.ini file, which can be found in C:\Windows\win.ini. We are going to take
a look at this file to help us understand more about it. So to help us out
more, open up the file C:\Windows\win.ini in Notepad.</p>
<font size="1">
<b>NOTE:</b> It's probably NOT a good idea to change any of the settings in this
file, as you can screw up your windows settings if you do. Your best and safest
bet is to copy the win.ini file to another location, and open it up from there.
Don't blame me if you dink around with this file and something goes wrong on your
machine. You've been warned.
</font>
<p>An INI File consists of three main part. The Section, the Key, and the Value.
If you browse through the win.ini file, you will see that it is split up into
"Sections". Each Section is defined by brackets. Beneath each Section is a list
of "Keys", and their respective "Values". Here is an example and explanation of
some Keys and Values from the Desktop Section of my win.ini file.</p>
[Desktop]<br>
Wallpaper=(None)<br>
TileWallpaper=0<br>
WallpaperStyle=2<br>
Pattern=(None)<br>
<p>In this example, our Section is called "Desktop". Beneath this, we have the
Keys "Wallpaper", "TileWallpaper", "WallpaperStyle", and "Pattern". Their respective
Values are "(None)", "0", "2", and "(None)". Your values are probably different than mine,
but the Keys should be the same. Every time Windows loads, the Operating System checks this
file, and creates your Desktop settings based on the values within this Section.</p>
<p>I can't really think of anything else to write to explain this any better, so I am
going to just jump ahead to using the TINIFile object within your Delphi project.</p>
<b>Part 2: TINIFile Object - Borland Loves You</b>
<p>Like many programmers, I once too struggled with the unholy carnage that was using the
Windows API in Visual Basic. Then one day, I heard about Delphi. After messing around with a
copy of it at a friends house, I found that all the things that were absolutely annoying and tedious about
Visual Basic could be done about 100 times faster and more efficiently in Delphi. I had seen the light at the
end of the tunnel, and it was being tended by the good people at Borland. They took the lame task of dealing with
INI Files and put it all into one, easy to use object.</p>
<p>The first thing we are going to do to enable the ability to read and write to INI Files in our
project is to put the word "INIFiles" into the Uses section of our main unit. Example:</p>
<font color="#008000">
uses <br>
Windows, Messages, SysUtils, Variants, Classes, Graphics, Controls, Forms,
Dialogs, StdCtrls,<b> INIFiles</b></font>;
<p>Let's go ahead and put a text box and two buttons onto our form. Name the text box
"txtValue". Name the Buttons "btnRead" and "btnWrite", and set their Captions to "Read INI"
and "Write INI" respectively. Create an "onClick" event for your btnWrite button, and insert the
following code.</p>
<p>
<font color="#008000">
TForm1.btnWriteClick(Sender: TObject); <br>
var<br>
&nbsp;&nbsp;&nbsp;&nbsp;myINI : TINIFile;<br>
begin <br>
&nbsp;&nbsp;&nbsp;&nbsp;myINI := TINIFile.Create(ExtractFilePath(Application.EXEName) + 'myinifile.ini');<br>
&nbsp;&nbsp;&nbsp;&nbsp;myINI.WriteString('Settings', 'Text Box', txtValue.Text);<br>
&nbsp;&nbsp;&nbsp;&nbsp;myINI.Free;<br>
end;
</font>
</p>
<p>
The first thing this code does is assign myINI as a TINIFile object. The .Create() is telling us that "Hey, everything
within these parentheses is the path to our INI File." I have used "ExtractFilePath(Application.EXEName) + 'myinifile.ini'".
This is telling us that our INI File will be located in the application's directory. Feel free to change this path if you wish.
If the file doesn't exist, don't worry. Delphi will automatically create the INI File once we call our next bit of code.</p>
<p>
The second thing this code does, is to write out a Value to a specific Key within a certain Section. The Section we are writing to
here is 'Settings', although realistically, it could be called anything you want. The second parameter is telling Delphi that
we want to write out a Key called 'Text Box'. Again, this can be anything you want it to be. Finally, the last parameter is
our Value for the Key 'Text Box', in the Section 'Settings'. In this example, it will write out whatever is contained within txtValue.Text.
</p>
<p>
Now that we have successfully written to a INI File, let's read it back in. Create an "onClick" even for your btnRead button and insert the following
code. :
</p>
<p>
<font color="#008000">
TForm1.btnReadClick(Sender: TObject); <br>
var<br>
&nbsp;&nbsp;&nbsp;&nbsp;myINI : TINIFile;<br>
begin <br>
&nbsp;&nbsp;&nbsp;&nbsp;myINI := TINIFile.Create(ExtractFilePath(Application.EXEName) + 'myinifile.ini');<br>
&nbsp;&nbsp;&nbsp;&nbsp;txtValue.Text := myINI.ReadString('Settings', 'Text Box', 'Default');<br>
&nbsp;&nbsp;&nbsp;&nbsp;myINI.Free;<br>
end;
</font>
</p>
<p>
Basically, the first line of code does the same thing as the btnReadClick event. If the file doesn't exist, don't worry.
The next line of code is a bit different than the WriteString procedure, however. Like the WriteString procedure, it is
going to look for the Section 'Settings', and the Key 'Text Box'. However, our third parameter is different. This parameter
is what will be returned if the Key 'Text Box' or Section 'Settings' doesn't exist. It will also return this if there is no
INI File to begin with. So if the Key exists, whatever is contained within it will be placed into the txtValue. If it doesn't,
then the word 'Default' will be put there.</p>
<p>Part 3: Other Types Of Procedures and Functions..</p>
In addition to reading and writing strings to/from INI Files, we can also read/write Integers, using "ReadInteger()" and "WriteInteger()" respectively.
There are also a slew of other procedures and functions that we can use. </p>
<ul>
	<li>DeleteKey</li>
	<li>EraseSection</li>
	<li>ReadBinaryStream</li>
	<li>ReadBool</li>
	<li>ReadDate</li>
	<li>ReadDateTime</li>
	<li>ReadFloat</li>
	<li>ReadSection</li>
	<li>ReadSections</li>
	<li>ReadBinaryStream</li>
	<li>ReadSectionValues</li>
	<li>ReadTime</li>
	<li>SectionExists</li>
	<li>WriteBinaryStream</li>
	<li>WriteBool</li>
	<li>WriteDate</li>
	<li>WriteDateTime</li>
	<li>WriteFloat</li>
	<li>WriteTime</li>
	<li>UpdateFile</li>
	<li>ValueExists</li>
</ul>
<p>Hopefully this will help you along your way with using INI Files. If you want an indepth description of what each
function, procedure, method, or event does, check the Delphi Help files.</p>
</font>

