<p align='middle'>
<font size='7' face='Century Gothic'><b><a href='http://raick.googlecode.com/files/RAICK.lua'>GET LATEST</a></b></font><br><br><br><br>
<p align='middle'>
<font size='7' face='Century Gothic'><b><a href='http://code.google.com/p/raick/wiki/GettingStarted#Installation'>How to Install ››</a></b></font><br><br>
<br><br>
<font size='5' face='Century Gothic'><b><a href='http://code.google.com/p/raick/downloads/list'>Show All Downloads ››</a></b></font>
<br><br>
<h1><font color='#003366' face='Century Gothic'>Change Log</font></h1>
<hr />
<h3><font color='#A30000' face='Century Gothic'>14.01.13</font> | <font color='#A30000'>Project Closed</font></h3>
Well, as you might have seen, the project has not been updated for a year, so I am officially closing it, since I don't have the time nor the interest to continue it. Thank you all who have used and continues to use RAICK! See ya!<br>
<h3><font color='#A30000' face='Century Gothic'>28.01.12</font> | <font color='#006600'>2.3.0</font></h3>
<ul><li>Homunculi S are now fully supported. I cannot test them myself as I am not playing on official servers, so do expect bugs. Any feedback and bug reports from iRO players is highly appreciated.<br>
</li><li>Added <code>Kagerou</code> and <code>Oboro</code> job recognition.<br>
<h3><font color='#A30000' face='Century Gothic'>22.12.11</font> | <font color='#006600'>2.2.1</font></h3>
</li><li>Removed <code>expand</code> method from <code>List</code> object. Now all methods are available upon creation of the object. It is advised to either delete the <code>[0] Memory.lua</code> file or reinstall the framework.<br>
</li><li>Added <code>put</code> method to <code>List</code> object.<br>
</li><li>Added <code>blank</code> query to <code>is</code> method of <code>Actor</code> object.<br>
</li><li>Fixed a bug in <code>mergeList</code> method of <code>List</code> object.<br>
<h3><font color='#A30000' face='Century Gothic'>18.09.11</font> | <font color='#006600'>2.2.0</font></h3>
</li><li>Added support for Homunculus S skills. This is another preparation step i.e. Homunculi S will work only partially with RAICK after this update. Please, read the <a href='http://code.google.com/p/raick/wiki/GettingStarted#AI_Specific_Files'>subsection about homunculus skill files</a> to get yourself acquainted with changes to the file structure. It is also a good idea to read the updated <a href='http://code.google.com/p/raick/wiki/Manual#Skill'>Skill object description</a> in the manual.<br>
</li><li>Changed the way skill handlers are distributed among skill files in the <code>Mercenary AI</code>. Now there is no <code>Common</code> skill file, instead all targeted skills that can be used by a particular type of mercenary are put directly in its file e.g. if before you had to define different behaviors for skill <code>Crash</code> for <code>Lancer</code> and <code>Fencer</code> in the <code>Common</code> skill file, then now each of them has its separate handler for that skill in its own skill file.<br>
</li><li>Added <code>mutated</code> query to <code>is</code> method of <code>Value</code> object.<br>
</li><li>Fixed the bug that caused errors when subtracting a vector from a cell.<br>
</li><li>Added a totally new and unique feature called <i>Quick Reload</i>. Read more <a href='http://code.google.com/p/raick/wiki/Manual#Quick_Reload'>here</a>.<br>
</li><li>For the framework to work correctly you must reinstall it.<br>
<hr />
<h3><font color='#A30000' face='Century Gothic'>27.08.11</font> | <font color='#006600'>2.1.0</font></h3>
</li><li>Fixed buggy error location tracking code.<br>
</li><li>Added Homunculus S ID's and names for probable future update.<br>
</li><li>Added custom mercenary support.<br>
<ul><li><i>Note: Some skill handlers have moved to the <code>Common Skills</code> file due to the fact that they are now used also by the new mercenaries. This is not a problem, since you can define any handlers in any file, but if you would like to update your skill files simply backup your AI and reinstall it. After that you can copy/put everything in its place.</i>
</li></ul></li><li>Added 3<sup>rd</sup> job support.<br>
</li><li>Added <code>mob</code> query to <code>is</code> method of <code>Actor</code> object(works also with <code>Mercenary AI</code>).<br>
</li><li><code>"Morroc Flying"</code> mob is renamed to <code>"Morroc Winged"</code>.<br>
</li><li>Made some other improvements to the inner structure.<br>
<hr />
<h3><font color='#A30000' face='Century Gothic'>10.05.11</font> | <font color='#006600'>2.0.3</font></h3>
</li><li>After extensive field testing I've found some very annoying bugs that made the framework practically unusable. Now they are fixed.<br>
</li><li>I've had plans to add custom mercenaries, Homunculus S skills and 3<sup>rd</sup> job recognition, but since the project is highly unpopular I've found it a waste on time(at least at this point). If you really like the framework and want to use it with the new stuff, then send <a href='http://forums.irowiki.org/member.php?u=15157'>me</a> a PM on <i>iRO Wiki Forum</i>. Maybe I'll reconsider <b>;)</b>
<hr />
<h3><font color='#A30000' face='Century Gothic'>23.01.11</font> | <font color='#006600'>2.0.2</font></h3>
</li><li>Fixed some bugs regarding actor classification by group and by type.<br>
<hr />
<h3><font color='#A30000' face='Century Gothic'>29.12.10</font> | <font color='#006600'>2.0.1</font></h3>
</li><li><code>List</code> and <code>Map</code> objects now also have <code>is</code> methods.<br>
</li><li>Minor bug fixes and performance enchantments.<br>
<hr />
<h3><font color='#A30000' face='Century Gothic'>13.11.10</font> | <font color='#006600'>2.0.0</font></h3>
</li><li>Release of the full version(still needs some testing).<br>
<hr />
<h3><font color='#A30000' face='Century Gothic'>04.10.10</font> | <font color='#006600'>2.0.0 beta</font></h3>
</li><li>Beta version released.<br>
<hr />