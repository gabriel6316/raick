# <font color='#003366'>Getting Started</font> #
## <font color='#006666'>Installation</font> ##
First things first, you need to let RAICK install itself. Unlike other AI scripts, RAICK is packaged into a single file. This file contains all of the logic needed to create the initial folder and file structure.<br>
<ul><li>To install RAICK you first need to decide where to put it. A typical place for custom scripts is the <code>USER_AI</code> folder, but you are not limited to a specific place. Once the <code>RAICK.lua</code> file is in place, open your <code>AI.lua</code> or <code>AI_M.lua</code> file in either <code>AI</code> or <code>AI/USER_AI</code> folder(depending on what <b>/hoai</b> or <b>/meai</b> setting you are planning to use) and put a single line of code there(all other code must be removed):<br>
</li></ul><blockquote><pre><code><br>
require "./AI/USER_AI/RAICK.lua"<br>
</code></pre>
This line of code assumes that you have put <code>RAICK.lua</code> into the <code>USER_AI</code> folder. The dot represents the folder of your Rangarok client. You could have also written the full path to RAICK:<br>
<pre><code><br>
require "C:/Program Files/Gravity/Ragnarok/AI/USER_AI/RAICK.lua" -- Of course, you should put the actual path to your client if it is somewhere else<br>
</code></pre>
And as I said you are not limited to your client folder only:<br>
<pre><code><br>
require "C:/RAICK.lua"<br>
</code></pre>
In this case all files and folders will be created right on the <code>C:/</code> disk.<br>
</blockquote><ul><li>Once <code>RAICK.lua</code> is linked with the <code>AI.lua</code> or <code>AI_M.lua</code> file you'll just need to launch the script from the game(activate your homunculus/mercenary). For a moment you will see a command-prompt window indicating that the installation has been performed.<br>
</li><li>When a new version of RAICK is released you'll just need to replace the <code>RAICK.lua</code> file to update the framework.<br>
<br>
<hr />
<h2><font color='#006666'>Files & Folders</font></h2>
The image below illustrates the full set of files and folders that RAICK can create:<br>
<br><br>
<img src='http://img148.imageshack.us/img148/2583/filesy.png' align='left' />
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
Most of them are created during installation, others during runtime, when needed. You can see that homunculus and mercenary scripts are separated into different folders for easier management.<br><br>
<h3><font color='#006600'>Common Files</font></h3>
</li><li><u><b>RAICK.Bugz.txt</b> file</u>
</li></ul><blockquote>This file is created(and later updated) when RAICK encounters a bug inside itself. The entry will contain the time when the error occurred and a copy of the error window. This is possible, because RAICK is smart enough to classify errors and can even distinguish errors that occurred in your script from the ones that occurred inside the framework.<br>
</blockquote><ul><li><u><b>RAICK.Settings.lua</b> file</u>
</li></ul><blockquote>This file is used to configure RAICK. See <a href='http://code.google.com/p/raick/wiki/GettingStarted#Settings'>Settings</a> for more information.<br>
</blockquote><ul><li><u><b>RAICK.Uninstaller.bat</b> file</u>
</li></ul><blockquote>Run this file if you want to uninstall RAICK. All files that have been created during installation will be deleted.<br>
<h3><font color='#006600'>AI Specific Files</font></h3>
</blockquote><ul><li><u><b>Homunculus AI</b> folder</u>
</li></ul><blockquote>The structure of the folder is designed for maximum efficiency and convenience. Files are numbered to mimic the order, in which they are loaded upon startup of the AI and also how they are processed later, when the client starts calling the script e.g. the framework would check for commands and skills before it launches the current activity.<br>
<ul><li><u><b>Logs & Errors</b> folder</u><br><br>
<ul><li><u><b>Error History.txt</b> file</u>
</li></ul><blockquote>This file is created(and later updated) when RAICK encounters an error inside your script. The entry will contain the time when the error occurred and a copy of the error window.<br>
</blockquote></li><li><u><b><code>[</code>0<code>]</code> Memory.lua</b> file</u>
</li></ul><blockquote>In this file RAICK stores values that you have decided to save. Saving data to a file is the only way to prevent it from being lost when the AI stops working(your homunculus/mercenary is not longer on the screen).<br>
</blockquote><ul><li><u><b><code>[</code>1<code>]</code> On Startup.lua</b> file</u>
</li></ul><blockquote>In this file you define your custom variables or functions that you want to use in your script. This file is loaded once when the script starts. It is typical place for reading saved data from the memory or putting initial values to variables.<br>
</blockquote><ul><li><u><b><code>[</code>2<code>]</code> Commands.lua</b> file</u>
</li></ul><blockquote>This is the place where you can define your own custom ways to interpret <i>Alt/Ctrl + Something</i> commands that come from the player. Default handlers are auto-generated so you just have to modify them.<br>
</blockquote><ul><li><u><b><code>[</code>3<code>]</code> XXX Skills.lua</b> file</u>
</li></ul><blockquote>Files with the same structure as the previous one, only here you can customize the way skill commands are interpreted by your AI. In the first file you must define skills of ordinary homunculi. Other files are used with mutated homunculi. Once you mutate your homunculus the first file will no longer be used, instead you should use the file with the type of your new homunculus. In this file you will find all skills of normal homunculi plus the skills of the corresponding mutated homunculus.<br>
</blockquote><ul><li><u><b><code>[</code>4<code>]</code> Messages.lua</b> file</u>
</li></ul><blockquote>In this file you can also define handlers like in two previous ones, but in this case they are meant to intercept messages that bots send to each other. This is a unique feature of RAICK that allows exchanging arbitrary data between homunculus and mercenary AI's.<br>
</blockquote><ul><li><u><b><code>[</code>5<code>]</code> Activities.lua</b> file</u>
</li></ul><blockquote>The "heart" of your AI. Here you must define activities that you want your homunculus/mercenary to perform. Activities(also known as <i>states</i> in most AI's) is just a way of dividing your script into logical parts. Each activity is, basically, a set of actions, which are logically grouped under some name. For example, the basic set of activities could be:<br>
<ul><li><i>Passive</i> - Don't react to anything. Just follow the owner.<br>
</li><li><i>Active</i> - If a monster is in sight then start chasing it(switch to <i>Chase</i> activity), if not then follow owner.<br>
</li><li><i>Chase</i> - Chase the monster until you get close enough and then start attacking it(switch to <i>Attack</i> activity).<br>
</li><li><i>Attack</i> - Attack the monster until it is killed or no longer in sight and then start looking for the next one(switch to <i>Active</i> activity).<br>
</li></ul>Now, all you need to do is put these words into code and you have yourself a primitive AI.<br>
</blockquote></blockquote><ul><li><u><b>Mercenary AI</b> folder</u>
</li></ul><blockquote>This folder basically mirrors the <b>Homunculus Script</b> folder. The only difference is in the <code>Skills</code> files: there is one file per type of normal mercenary and a separate file for all skills of monster mercenaries.<br><br>
<hr />
<h2><font color='#006666'>Settings</font></h2>
RAICK can be configured using the <code>RAICK.Settings.lua</code> file. Currently RAICK has 4 settings:<br>
</blockquote><ul><li><b>VisionRange</b>
</li></ul><blockquote><u>Default:</u> <code>14</code><br>
<u>Supported values:</u> <code>number &gt;0</code><br></blockquote>

<blockquote>The distance between your character and the visible edge of the screen(not the one you can see if you zoom out, but the one where objects on the ground, players, monsters etc are no longer visible). Typically it is 14 cells, but if you play on some unique server, then it might be different.<br>
</blockquote><ul><li><b>Language</b>
</li></ul><blockquote><u>Default:</u> <code>EN</code><br>
<u>Supported values:</u> <code>EN, RU</code><br></blockquote>

<blockquote>Currently RAICK supports only English and Russian. This setting affects mainly error messages.<br>
</blockquote><ul><li><b>LoggersUseTraceAI</b>
</li></ul><blockquote><u>Default:</u> <code>NO</code><br>
<u>Supported values:</u> <code>YES, NO, ON, OFF</code><br></blockquote>

<blockquote>Defines whether Logger objects react to <b>/traceai</b> command status. This setting is used for <a href='http://code.google.com/p/raick/wiki/Manual#Logger'>Loggers</a>.<br>
</blockquote><ul><li><b>BotCommunication</b>
</li></ul><blockquote><u>Default:</u> <code>OFF</code><br>
<u>Supported values:</u> <code>YES, NO, ON, OFF</code><br></blockquote>

<blockquote>Turns communication between homunculus and mercenary ON or OFF. Explained <a href='http://code.google.com/p/raick/wiki/Manual#Data_Exchange_Between_Homunculus_and_Mercenary'>here</a>.<br>
</blockquote><ul><li><b>QuickReload</b>
</li></ul><blockquote><u>Default:</u> <code>ON</code><br>
<u>Supported values:</u> <code>YES, NO, ON, OFF</code><br></blockquote>

<blockquote>Turns the <code>Quick Reload</code> feature ON or OFF. Explained <a href='http://code.google.com/p/raick/wiki/Manual#Quick_Reload'>here</a>.<br>
The names of settings and the values that they support are case insensitive, furthermore you can even separate different words and letters with underscores. For example:<br>
</blockquote><ul><li>visionrange<br>
</li><li>ViSion<code>___</code>RanGE<br>
</li><li>VISI_ON<code>_</code>RAN_GE<br>
</li><li>VisionRange<br>
Would all refer to the same setting. The same is with values:<br>
</li><li>Yes<br>
</li><li>No<br>
</li><li>On<br>
</li><li>Off<br>
</li><li>ON<br>
</li><li>OfF<br>
Are all permitted. It does not matter if you write <code>'ON'</code> or <code>ON</code> inside this file, since variable names are translated into strings.<br>
And one more thing- if you omit/delete some setting the default value will be used. All of this is done for your convenience.<br><br>
<hr />
<h2><font color='#006666'>Try It Out!</font></h2>
The best way to learn something in programming is by doing practical exercises or writing something yourself, so let's write a simple AI using RAICK. This way by the end of this chapter you will have both a working script and an idea of whether RAICK actually suits your needs.<br><br>
<hr />
<h3><font color='#006600'>Some Extra Knowledge: Objects in RAICK</font></h3>
As much as I(and I guess you too) would like to dig into the scripting process right away I can't leave this topic without attention, since roughly it is what RAICK is made of.<br>
From the <a href='http://code.google.com/p/raick/wiki/Lua#The_Hard_Part:_Objects_and_Primitive_Types'>chapter about Lua</a> you know that an <i>object</i> is a value, which is stored in a variable <b>by reference</b>. The same is true for RAICK objects(and pretty much for all objects in every modern programming language), but in the traditional meaning the <i>object</i> is not only some value that stores its reference in a variable, but an advanced entity of data, which(unlike primitive values) can itself contain data and operations that work with this data. It can be seen as a way to group related data and actions that you can perform on this data under some general idea. Let me just explain this by comparing the way of Gravity with the way of RAICK:<br>
<pre><code><br>
-- This is a standard function from Gravity, which allows us to order the homunculus to go to a cell with (x,y) coordinates.<br>
-- 'homunID' is the ID of your homunculus and (x,y) are coordinates of the destination cell.<br>
Move(homunID, x, y)<br>
<br>
-- Now let's observe how it is done in RAICK:<br>
Homunculus.goTo(object)<br>
-- Do you remember that I had mentioned something about the syntax 'something.something(arg1, arg2, ...)'?<br>
-- Well, here it is. This is just a way to call inner functions of objects. Those functions are called "methods".<br>
-- A method is like any other function, but the difference is that it is a "property" of the object and is linked with its data.<br>
<br>
-- And one more pair:<br>
Attack(homunID, targetID)<br>
<br>
Homunculus.hit(target)<br>
</code></pre></li></ul>

You can see that instead of writing a lot of separate functions that take their the ID as their first argument we can create a generalized concept- an object of type <code>Homunculus</code>. This object can be used to hold the data(like the type of your homunculus or its location) and the actions/commands associated with this data or with the concept itself(like methods to order your homunculus to move to some cell or use a skill). It is as almost we were saying:<br>
<blockquote><i>Homunculus, do that</i><br>
Instead of:<br>
<i>Function, make homunculus with this ID do that</i><br>
This approach allows us to have a more organized, understandable and maintainable code and that is why objects are used in programming.<br>
So, let's now sum up everything that we know about objects(as a general concept in programming):<br>
</blockquote><ul><li>Are values that are stored in variables as references<br>
</li><li>Are created using a special command/function(that can also take arguments as you will see later)<br>
</li><li>Can contain functions inside themselves(those functions are called <i>methods</i> and in Lua they are just function values under string keys in a table)<br>
</li><li>Can contain any other type of data inside themselves(the places, where this data is stored are called <i>fields</i> and in Lua they are just string keys in a table)</li></ul>

From this section you also need to remember that there is a difference between the <i>object</i> as a general concept in programming and those objects that exist in Lua. In Lua the word <i>object</i> could mean one of two things:<br>
<ul><li>Just a value that is stored in the variable as a reference(for example, functions)<br>
</li><li>The implementation of the general concept using stuff that Lua has(for example, RAICK objects are designed using almost every data type available to fit the list features that this general concept declares)<br>
There are actually a lot of other features that a true object should have, but I did not want to make them too complex, so they are sort of like a lightweight option.<br>
<br><br>
<hr />
<h3><font color='#006600'>The Initial Idea</font></h3>
Now that RAICK objects is smaller mystery for us we can, finally, start thinking about our script. First of all, you need to have a clear idea of what you want from your AI. Every AI has a main purpose and this purpose defines the principles that you will use when creating it. Will it be for PvP or for mob killing only or maybe you would like to make a tank out of your homunculus/mercenary that would try to provoke monsters on itself. Of course, it is easy to say that: "I want it to be as cool as RampageAI!", but wouldn't it be easier then just to use Rampage instead? RAICK is not meant(but still can be used) to build super-complex AI's that do everything, because those AI's are already created and I don't think that you can make something even close to AzzyAI or RAIL, not speaking of writing a better one. Instead RAICK gives you, on the one hand, a way to get into the scripting process with less pain and, on the other hand, the possibility to write small scripts that 100% fulfill your current needs. When your needs change, your script will change with them. This way you can initially write yourself a very simple script and modify it as your needs and your skills in programming will grow. Small, but constant changes to your script- that is the pattern I recommend following, when creating your AI using RAICK.<br>
So, going back to the idea. Let's create a script for homunculus Vanilmirth that would allow us to:<br>
</li></ul><ol><li>Give homunculus orders to attack a specified target using both Caprise and normal attacks<br>
</li><li>Auto-attack those who are damaging your character or homunculus and use caprise on those, who cast something on us(excluding support skills)<br>
</li><li>Switch between active and passive modes<br>
Those 3 objectives now give us something to move further and start writing our first lines of code.<br><br>
<hr />
<h3><font color='#006600'>First Lines of Code</font></h3>
Let's move to our workplace- the <code>Homunculus AI</code> directory. Open the <code>On Startup</code> file. Here we can initialize(put initial values to) the variables that we are going to use. This is not entirely needed, but it allows us to eliminate the need to check our variables later in the code. Right now the only one we will need is the one, where we would store our target. So we write:<br>
<pre><code><br>
mainTarget = Actor()<br>
-- 'Actor()' is a constructor for the object 'Actor', which represents all objects that your homunculus/mercenary can see(monsters, players, NPCs).<br>
-- Normally, you would pass the ID of the object as an argument, but here we don't do it and as a result we get a "blank" Actor object.<br>
-- The blank actor represents the absence of one, like 'nil' the absence of any value, but when the variable is meant to store actors ..<br>
-- .. it is better to use this value instead of 'nil' as you will see later.<br>
</code></pre></li></ol>

What we have done is we have put a blank actor as a default value for the target. It is the first/initial value that this variable will have when the script starts and it will signal that we have not got a target at the moment. If we haven't had done this, then the default value would have been <code>nil</code>, which would force us to check this variable for <code>nil</code> every time we read it.<br>
The first step is made, let's now turn to the "main course"- the <code>Activities</code> file. As you can see one activity is already defined here. It serves mainly as an example. In this activity your homunculus would just follows you. This is obviously too simple for us so let's modify it.<br>
To begin we need at least 2 activities:<br>
<pre><code><br>
function    Main()<br>
<br>
Homun.goTo(Owner)<br>
end<br>
<br>
function    FollowOwner()<br>
<br>
Homun.goTo(Owner)<br>
end<br>
-- The 'Homun' variable holds the object of type Homunculus. As you might have already guessed it represents your homunculus.<br>
-- In the auto-generated activity 'FollowOwner' the variable 'Homunculus' was used instead, which you can also use.<br>
-- For your convenience references to this object are stored in variables starting from 'Hom' and ending with 'Homunculus'.<br>
-- So, for example, 'Homu' or 'Homunc' can also be used.<br>
</code></pre>

Right now they are identical, but later we will start changing the first one. Before we do that we must provide ourselves with a way to switch between active(represented by activity <code>Main</code>) and passive(represented by activity <code>FollowOwner</code>) modes. This is done in the <code>Commands</code> file. You can see that this file is also filled with auto-generated functions. In programming those functions are called <i>handlers</i>, because they are meant to <i>handle</i> certain signals that come from the outer or inner environment(in our case from the client) of your program. One of the methods to bind a handler function with the corresponding signal is by using predefined names and this is the method that RAICK uses:<br>
<pre><code><br>
-- When a function in this file is named 'AltT' or 'altt' or even 'ALT_T'(case and underscores do not play any role), then RAICK binds it with the command 'Alt + T'.<br>
function    AltT()<br>
<br>
if Activity.current.is.Main then -- If our current activity is 'Main', then ..<br>
Activity.switchTo.FollowOwner() -- .. we change it to 'FollowOwner'<br>
else -- If not, then ..<br>
Activity.switchTo.Main() -- .. we change it to 'Main'<br>
end<br>
end<br>
</code></pre>

I think already from this short piece of code you can see how easy it is to use and understand RAICK. Let me explain I little bit what is happening here. What we do is we read the field <code>current</code> of the <code>Activity</code> object(which is located in the global variable <code>Activity</code>). This field contains another object of type <code>Value</code>. For now, all you need to know about this object is that it holds a name in form of a string and this string can be compared with some other string using a very convenient method <code>is</code>. That's right! It is a method, but not a regular one, since it allows you to write this:<br>
<pre><code><br>
something.is.name<br>
</code></pre>
Instead of:<br>
<pre><code><br>
something.is("name")<br>
</code></pre>

The first variant in definitely easier to read and faster to write. Most of RAICK's objects have this method(and its opposite "twin brother" <code>isNot</code>) in common and later I will show you what other tricks can be performed using it.<br>
If we drop the technical details, then what <code>Activity.current.is.Main</code> does is it just gives us <code>true</code> if current activity is <code>Main</code>. Quite obvious, isn't it? Other lines are also pretty much self-explainable. The <code>switchTo</code> field contains a table, which holds functions that allow us to switch between activities.<br>
So, we can change modes now, but that doesn't give us anything without a target to attack, since passive mode is made mainly to stop homunculus/mercenary from attacking the target. We will deal with this issue in the next section.<br>
<br><br>
<hr />
<h3><font color='#006600'>Manual Target Selection</font></h3>
There are many ways to tell your bot to attack something. If it doesn't have any targeted skills(for example, <i>Lif</i> or <i>Amistr</i>), then basically the only choice you have is clicking near the target and ordering your bot to attack the closest actor to this cell. Luckily, our <i>Vanilmirth</i> has got <i>Caprise</i> and we can use it directly to select targets.<br>
Let's do it then! Open <code>Skills</code> file. As always in RAICK handlers are already defined and default actions are set. What you need to do is redefine the handler for <i>Caprise</i>:<br>
<pre><code><br>
-- 'target' is an argument that this handler receives.<br>
-- This variable holds the 'Actor' object that represents the monster or player, on which you have used the skill 'Caprise'.<br>
-- And as you might have already guessed argument 'level' holds the level of the skill used.<br>
function    Caprise(target, level)<br>
<br>
mainTarget = target<br>
end<br>
</code></pre>
Nothing to comment here.<br><br>
<hr />
<h3><font color='#006600'>Back to Our Activities</font></h3>
The preparational work is done, it is now time to think about how we are going to use the selected target. Obviously, we want to kill it. I propose that we make another activity just for this cause:<br>
<pre><code><br>
function    Main()<br>
<br>
-- This is the place, where using a blank actor instead of leaving the variable uninitialized pays off.<br>
-- If we hadn't initialized the variable, then we would have been forced to check if 'mainTarget ~= nil' every time we wanted to use the variable.<br>
if mainTarget.status.is.visible and mainTarget.action.isNot.dead then -- If the target is visible and not dead, then ..<br>
Activity.switchTo.AttackMainTarget() -- .. we lock on it to kill.<br>
else -- If not, then ..<br>
Homun.goTo(Owner) -- .. we just follow the owner.<br>
end<br>
end<br>
<br>
function    AttackMainTarget()<br>
<br>
if mainTarget.status.isNot.visible or mainTarget.action.is.dead then -- If the target is not visible anymore or is already dead, then ..<br>
Activity.switchTo.Main() -- .. there is no point in performing this activity anymore and we can return to from where we came.<br>
else -- If the target is still with us, then ..<br>
-- 1) We follow it no matter what<br>
Homun.goTo(mainTarget)<br>
<br>
-- 2) Use 'Caprise', if we are close enough<br>
if Homun .. mainTarget &lt;= Caprise.range then<br>
Homun.use(Caprise).on(mainTarget)<br>
end<br>
<br>
-- 3) Hit/bite the target, if we are close enough<br>
if Homun .. mainTarget &lt;= Homun.hit.range then<br>
Homun.hit(mainTarget)<br>
end<br>
end<br>
end<br>
<br>
function    FollowOwner()<br>
<br>
Homun.goTo(Owner)<br>
end<br>
</code></pre>

In the <code>Main</code> activity we check if the target is visible(can be visually observed on the screen) and if it is not dead(it might be confusing that being dead is an action, but you should just accept this for now), then we switch to our "killing activity".<br>
In the <code>AttackMainTarget</code> activity we check for the opposite: if the target is not visually observable or it is dead, then all is left for us is to go back to from where we came. A lot more interesting part for us lies in the <code>else</code> scenario. First of all, when the target is available, the homunculus will follow it. Secondly, it will use <i>Caprise</i> on the target if the distance between the homunculus and the target is less equal than the range of the skill. And finally, our <i>Vanilmirth</i> will "bite" the target if it is in range of the hit.<br>
With so little lines of code we already have ourselves a primitive, but nonetheless a working AI! So far, we have implemented 2 out of 3 ideas.<br>
In the next section we will make an attempt to complete our AI by adding the auto-attack functionality.<br><br>
<hr />
<h3><font color='#006600'>Automated Target Selection</font></h3>
To implement this feature we need to update both <code>Main</code> and <code>AttackMainTarget</code> activities. Let's start with <code>AttackMainTarget</code>:<br>
<pre><code><br>
function    AttackTarget(target)<br>
<br>
if target.status.isNot.visible or target.action.is.dead then -- If the target is in not the memory or it is not visible anymore or is already dead, then ..<br>
Activity.switchTo.Main() -- .. there is no point in performing this activity anymore and we can return to from where we came.<br>
else -- If the target is still with us, then ..<br>
-- 1) We follow it no matter what<br>
Homun.goTo(target)<br>
<br>
-- 2) Use 'Caprise', if we are close enough<br>
if Homun .. target &lt;= Caprise.range then<br>
Homun.use(Caprise).on(target)<br>
end<br>
<br>
-- 3) Hit/bite the target, if we are close enough<br>
if Homun .. target &lt;= Homun.hit.range then<br>
Homun.hit(target)<br>
end<br>
end<br>
end<br>
</code></pre>

There are 2 changes here: we have renamed <code>AttackMainTarget</code> to <code>AttackTarget</code> and added activity argument <code>target</code>, which is now used instead of <code>mainTarget</code>. Activity arguments are just like usual function arguments plus they are automatically saved to(and retrieved from) the memory.<br>
Let's now look at the modified <code>Main</code> activity to see how you can pass arguments to activities:<br>
<pre><code><br>
function    Main()<br>
<br>
if mainTarget.status.is.visible and mainTarget.action.isNot.dead then -- If the target is visible and not dead, then ..<br>
Activity.switchTo.AttackTarget(mainTarget) -- .. we lock on it to kill(observe how we pass 'mainTarget' as an argument).<br>
else -- If not, then ..<br>
for i, actor in Owner.surround.each() do -- .. we make a loop over the list of all visible actors. For each actor we check:<br>
if actor.target.is(Owner, Homun) then -- If its target is you or your homunculus and ..<br>
if actor.action.is.attacking then -- .. it is attacking someone(in other words, if it is attacking us), then ..<br>
Activity.switchTo.AttackTarget(actor) -- .. we attack it(observe how we now pass the filtered 'actor' as an argument).<br>
return -- We can use 'return' without any values just to stop a function at some point and it is very handy in this situation, since ..<br>
-- .. we don't want to do anything else.<br>
elseif actor.action.is.casting then -- .. it is not attacking, but is casting something(in other words, if it is casting something on us), then ..<br>
Homun.use(Caprise).on(actor) -- .. we just use 'Caprise' on it to interrupt the casting.<br>
-- Of course, if there are multiple casters, then we will interrupt only one of them and other commands will not be executed because of the delay.<br>
end<br>
end<br>
end<br>
end<br>
<br>
Homun.goTo(Owner) -- If we have not selected any targets to attack, then we just follow the owner.<br>
end<br>
</code></pre>

This is the first time you see how the <code>for</code> loop is used to scan through every visible actor. <code>Owner.surround.each()</code> work similarly to <code>ipairs</code> meaning that it passes actors(along with the index <code>i</code>) one by one to the loop. What you can also notice here is that we now specify the target through the argument of the <code>AttackTarget</code> activity and that we use <code>return</code> to interrupt the execution of the activity. This technique is very useful in cases when you have already switched to another activity and don't want the current activity to be executed anymore.<br>
At this moment we can say that all 3 planned features are implemented, but actually there are still some minor details that require our attention. We will have a look at them in the next section.<br><br>
<hr />
<h3><font color='#006600'>The Final Touch</font></h3>
The first issue concerns the fact that the main target we select is not saved to the memory. This could be easily fixed with a few modifications.<br>
In <code>On Startup</code> file:<br>
<pre><code><br>
-- We retrieve the record "mainTarget" upon startup of your AI. If it does not exists in the memory, we return a "blank" actor instead.<br>
mainTarget = Memory.get("mainTarget", Actor())<br>
</code></pre>
And in <code>Skills</code> file:<br>
<pre><code><br>
function    Caprise(target, level)<br>
<br>
mainTarget = Memory.save("mainTarget", target) -- Save the value from the variable 'target' under the name "mainTarget" and return this value afterwards.<br>
end<br>
</code></pre>

Once this is added we momentarily have created ourselves another problem: how do we erase the selected target from the memory if we don't want to attack it anymore? In our case the best way to do it is to put a blank actor to the "mainTarget" entry. We also need to think of signal to tell the AI that we want to do it. A click under the character, for example, could be a good choice. This means that we must modify the <code>Commands</code> file:<br>
<pre><code><br>
-- This handler is called, when the player presses 'Alt + Right Click On The Ground'<br>
function    AltGround(cell)<br>
<br>
if cell.is(Owner.cell) then -- If the clicked cell is the same cell as the one our character stands on, then ..<br>
mainTarget = Memory.save("mainTarget", Actor()) -- .. we clear both the variable and the entry in the memory.<br>
end<br>
end<br>
</code></pre>

The second thing that needs to be fixed is again located in the <code>Skills</code> file, which we have already update above. If you analyze the current code of the AI you would notice that if our homunculus is already attacking someone or it is in a "passive mode", then it would not react to the fact that we have selected a target. This is certainly not what we want, since it is the main target and the homunculus should respond immediately if we explicitly show it the enemy. To correct this we just add a line of code to the <code>Caprise</code> handler in the <code>Skills</code> file:<br>
<pre><code><br>
function    Caprise(target, level)<br>
<br>
mainTarget = Memory.save("mainTarget", target) -- Save the target and ..<br>
Activity.switchTo.AttackTarget(mainTarget) -- .. order to attack it right away.<br>
end<br>
</code></pre>
The third problem lies in the automated target selection part. Here we have forgotten to add a condition that would filter out actors that cast supportive magic on us. Unfortunately, there is no straight way to do it(you cannot get any data about the type of the skill that someone is casting). However, we can try to come up with a solution that would give us similar results like, for example, filtering out supportive jobs:<br>
<pre><code><br>
...<br>
-- Everything is the same, only now we also filter out full-support jobs.<br>
-- If a Soul Linker or a Priest is attacking us, then we should not waste our time on him.<br>
-- Full-supports also don't have any serious offensive skills, so if he is casting something on us it is most likely supportive magic.<br>
if actor.target.is(Owner, Homun) and actor.type.isNot(Priest, HighPriest, BabyPriest, SoulLinker) then -- 'is' and 'isNot' can take ..<br>
-- .. as many arguments as you like.<br>
if actor.action.is.attacking then<br>
Activity.switchTo.AttackTarget(actor)<br>
return<br>
elseif actor.action.is.casting then<br>
Homun.use(Caprise).on(actor)<br>
end<br>
end<br>
...<br>
</code></pre>

The final issue is very small, but could lead to a very annoying and confusing error. It lies in the <code>AttackTarget</code> activity(and pretty much every activity that uses arguments). As I have mentioned before, activity arguments are automatically saved to the memory preventing it from being vanished(turned to <code>nil</code>) upon the restart of the AI. But what if for some reason the memory is lost? The probability of that is very small, but nonetheless it can happen and thus this problem needs to be fixed. So, let's do it:<br>
<pre><code><br>
function    AttackTarget(target)<br>
<br>
-- In case the 'target' argument is 'nil'(it is not in the memory) we leave the activity.<br>
if target == nil or target.status.isNot.visible or target.action.is.dead then<br>
Activity.switchTo.Main()<br>
...<br>
</code></pre>
With this last addition we can finally say that the script is done! Enjoy your (most likely first) self-made AI!<br><br>
<hr />
<h3><font color='#006600'>It's Done!</font></h3>
In this short introductory guide I have shown you how a working AI could be created using RAICK. This page is not intended to teach you the details of how everything works, it is just an example of some of RAICK's core features. I can say that I have demonstrated only about 5-7% of what RAICK can really offer you. To learn the full potential of RAICK you need to get yourself acquainted with the <a href='Manual.md'>Reference Manual</a>.<br>
<br><br>
<hr />
<h3><font color='#006600'>Appendix</font></h3>
Below you will find the list of files for the AI that was created in this guide:<br>
<ul><li><a href='http://raick.googlecode.com/files/%5B1%5D%20On%20Startup.lua'>On Startup</a>
</li><li><a href='http://raick.googlecode.com/files/%5B2%5D%20Commands.lua'>Commands</a>
</li><li><a href='http://raick.googlecode.com/files/%5B2%5D%20Skills.lua'>Skills</a>
</li><li><a href='http://raick.googlecode.com/files/%5B2%5D%20Activities.lua'>Activities</a>