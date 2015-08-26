<p align='middle'>
<br>
<font size='7'>Become <font color='#660000' face='Century Gothic'><u><b>The Creator</b></u></font> !</font>
<br>
<br>
<br>
<p align='left'>
<font color='#003366' size='3'>
You are visiting the homepage of a unique Ragnarok AI project. Although, it is created for AI purposes, it is not really an AI. <b>RAICK</b> could be defined as a <b>framework</b> for AI creation. Now, this word may not be very familiar to you, but it is actually a very simple concept. This is a set of tools, which brings AI creation to a whole new level. It hides all the nerdy and complex programming stuff and in exchange gives a simple set of intuitive and easy-to-use instruments for you to program your homunculus/mercenary your way. As many framework developers like to say about their creations:<font color='#660000' size='3' face='Book Antiqua'>
<blockquote>It takes care of the "plumbing" leaving you to define only the things that really matter with minimum effort and time consumption</font></font>
<h2><font color='#006666'>For Newbies in Programming</font></h2>
So, to put it simple:<br>
</blockquote><ul><li>You can be interested in this project if:<br><br>
<ol><li>You want to learn how to program your homunculus/mercenary, but the standard way is too complex for you.<br>
</li><li>You would like to have more control over the actions of your homunculus/mercenary than just editing config files.<br>
</li><li>You want to learn how AI script functions.<br><br>
</li></ol></li><li>This tool is probably <b>NOT</b> for you if:<br><br>
<ol><li>The mere word "programming" makes you want to jump out of the window.<br>
</li><li>You are fully satisfied with what other AI's offer you.<br>
</li><li>You hate to learn new stuff.</li></ol></li></ul>

To put it even simpler, here is an ugly and scary piece of code from the default AI, which finds the closest monster attacking your character:<br>
<pre><code><br>
function    GetOwnerEnemy (myid)<br>
local result = 0<br>
local owner  = GetV (V_OWNER,myid)<br>
local actors = GetActors ()<br>
local enemys = {}<br>
local index = 1<br>
local target<br>
for i,v in ipairs(actors) do<br>
if (v ~= owner and v ~= myid) then<br>
target = GetV (V_TARGET,v)<br>
if (target == owner) then<br>
if (IsMonster(v) == 1) then<br>
enemys[index] = v<br>
index = index+1<br>
else<br>
local motion = GetV(V_MOTION,v)<br>
if (motion == MOTION_ATTACK or motion == MOTION_ATTACK2) then<br>
enemys[index] = v<br>
index = index+1<br>
end<br>
end<br>
end<br>
end<br>
end<br>
<br>
local min_dis = 100<br>
local dis<br>
for i,v in ipairs(enemys) do<br>
dis = GetDistance2 (myid,v)<br>
if (dis &lt; min_dis) then<br>
result = v<br>
min_dis = dis<br>
end<br>
end<br>
<br>
return result<br>
end<br>
</code></pre>
And here is its analogue written using RAICK:<br>
<pre><code><br>
function    GetOwnerEnemy ()<br>
<br>
local agressors = List()<br>
<br>
for i, enemy in Owner.surround.each() do<br>
if enemy.group.is.Mob and enemy.target.is(Owner) and enemy.action.is.Attacking then<br>
agressors.add(enemy)<br>
end<br>
end<br>
<br>
return agressors.closestTo(Owner)<br>
end<br>
</code></pre>
In the last one you can almost intuitively guess what the code chunk is doing. As for the default AI code, well, I think even one look at it makes you want to close the file and never touch it again. That's one of the main benefits of using RAICK- it does not scare you away. The framework provides a natural, close to human language way of writing your script. It brings AI programming closer to your, without limiting your possibilities.<br>
You can start with an <a href='Lua.md'>introduction to AI and Lua</a> to build a foundation for understanding and working with RAICK.<br><br>
<hr />
<h2><font color='#006666'>For Geeks and Those Just Familiar With the Craft</font></h2>
For those, who are already familiar with programming, here is what RAICK will offer your in terms of enhancing your AI scripting experience:<br>
<ul><li><font color='#660000'><b>Ready-to-use folder and file structure</b></font>
</li></ul><blockquote>Upon installation RAICK defines a simple file and directory layout. With only a few configuration nuances you can immediately engage in the scripting process.<br>
</blockquote><ul><li><font color='#660000'><b>Object-oriented design</b></font>
</li></ul><blockquote>RAICK provides you with a set of simple, but powerful objects, which categorize the data used in the AI and provide convenient ways to manipulate it. The data is collected and analyzed for you- just reach out to get it!<br>
</blockquote><ul><li><font color='#660000'><b>Handlers for player commands</b></font>
</li></ul><blockquote>Player commands are captured by handlers, which you don't even have to define- it is done for you. You just have to open the right file and customize them the way you like. What could be simpler than that?<br>
</blockquote><ul><li><font color='#660000'><b>Declerative state definition</b></font>
</li></ul><blockquote>States(which in RAICK are called Activities) are defined in the same way as handlers for player commands. You just have to define functions in a special file and they will automatically become your states. Switching between them is also done with one method call. Managing your states now takes just a fraction of the former time!<br>
</blockquote><ul><li><font color='#660000'><b>Names instead of ID's</b></font>
</li></ul><blockquote>With RAICK you can forget about ID's in your script. Everything is replaced with names. Every monster, every skill- you just have to name it.<br>
</blockquote><ul><li><font color='#660000'><b>Data persistence out of the box</b></font>
</li></ul><blockquote>Pretty much every data type used in the script can be serialized and retrieved upon startup of AI. This way you can prevent vital data(like targets and friend-lists) from being lost, when your script restarts. Preserving your crucial data has never been easier!<br>
</blockquote><ul><li><font color='#660000'><b>Smart error handling</b></font>
</li></ul><blockquote>RAICK catches any errors that occur in your script. The error window will appear only once, after which your homunculus/mercenary will enter the Safe Mode. The error window itself will contain more detailed information about the cause of the error and will be logged to a file. RAICK can even analyze errors and inform you if the error is caused by a bug inside RAICK. This way you can just paste the error log in a bug report and I will immediately have the information to fix it. You can kiss the annoying endless default error windows goodbye!<br>
</blockquote><ul><li><font color='#660000'><b>Exchange of data between your homunculus and mercenary</b></font>
</li></ul><blockquote>With the flip of a switch your bots immediately begin to communicate. Your homunculus will have full control over the actions of the mercenary and vice-versa. Programming different cooperation scenarios- with RAICK it's a piece of pie!<br>
</blockquote><ul><li><font color='#660000'><b>On-the-fly script update</b></font>
</li></ul><blockquote>Tired of being forced to "Rest-Summon" your homunculus or "Char Select" your mercenary after every little change? Well, with RAICK you can leave those memories behind, because <i>Quick Reload</i> feature allows you to see the changes as soon as you press <i>Save</i> in your text editor!<br>
If you want to get a feeling of RAICK I would advise you to read the <a href='GettingStarted.md'>Getting Started</a> page first, but if you feel like you want to learn more about Lua, then it is better to start with the <a href='Lua.md'>introduction to AI and Lua</a>.