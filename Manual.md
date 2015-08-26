# <font color='#003366'>Reference Manual</font> #
The reference manual is a highly detailed description of a product. It is often a very dry and concrete document, reading which can be quite boring. You can check out the [Lua documentation](http://www.lua.org/manual/5.1/manual.html) for an example of a typical reference manual.<br>
I will do my best to make this manual easily readable and understandable.<br>
<h2><font color='#006666'>Detailed Description of Objects</font></h2>
Objects are basically what RAICK is made of. About 80% of what the framework offers is in one way or another related to them. They are divided into 2 categories:<br>
<ul><li>Single objects<br>
</li></ul><blockquote>Exist only in a single exemplar, which is automatically created upon startup of your script.<br>
</blockquote><ul><li>Multipliable objects<br>
</li></ul><blockquote>Can be created an arbitrary number of times using the <i>constructor</i>, which is located in a global variable with the same name as the type of the object(for example, constructor for object <code>Cell</code> is located in the global variable <code>Cell</code>). The constructor is nothing more than a function and like any function it can take arguments(for example, <code>Cell(20,30)</code> creates a <code>Cell</code> object with coordinates (20,30)).<br>
Some objects allow operators to be used on them(you can distinguish them by the <u><b>Operators</b></u> subsection). For example, you may remember that we have used operator <code>..</code> to get the distance between your homunculus and its target in the <a href='http://code.google.com/p/raick/wiki/GettingStarted#Back_to_Our_Activities'>Getting Started</a> guide.<br>
You may also notice that the <u><b>Constructors</b></u> subsection is in plural. That is because objects can indeed have multiple constructors. Every constructor takes a different number/types of arguments and based on that produces an object with desired properties. A good example is the <a href='http://code.google.com/p/raick/wiki/Manual#Logger'>Logger</a> object.<br>
The <u><b><i>is</i> Methods</b></u> subsection is used to describe what types and values does the <i>is</i> group of methods understand for the current object. They are used to gain yes/no answers about the object. The group consists of 2 methods: <code>is</code> and <code>isNot</code>, which in turn have 2 forms, making a total of 4 methods. They can be described as follows:<br>
<ul><li>First form of <code>is</code> method:<br>
</li></ul><blockquote><code>object.is(value1, value2, value3, ...)</code>
</blockquote><ul><li>Second form of <code>is</code> method:<br>
</li></ul><blockquote><code>object.is.value</code>
</blockquote><ul><li>First form of <code>isNot</code> method:<br>
</li></ul><blockquote><code>object.isNot(value1, value2, value3, ...)</code>
</blockquote><ul><li>Second form of <code>isNot</code> method:<br>
</li></ul><blockquote><code>object.isNot.value</code>
The first form of the <code>is</code> method can receive an arbitrary number of arguments of any type, but only certain values have meaning for it. The method returns <code>true</code> if at least one of the given values(as if all arguments were grouped  with <code>or</code>) is "telling" the truth about the current object. If all given values are either "lying" or are unknown to the method it will return <code>false</code>. The second form does the same, but can take only one <code>string</code> argument, which is passed to the method in a very original and convenient way. For example, <code>actor.is.visible</code> is just another way of writing <code>actor.is("visible")</code>. Although the second form is more restricted it is nonetheless faster to write and far easier to read and that's why I decided to introduce it.<br>
The <code>isNot</code> method is the opposite of <code>is</code>. It returns <code>true</code> if all given values are "lying" about the current object or are unknown to the method and <code>false</code>, if at least one of the value is "telling" the truth.<br>
<br>
Last thing worth mentioning is that all string argument are case insensitive meaning that, for example, <code>actor.is("VISiBLe")</code> or <code>actor.is.ViSiBle</code> would also be accepted. Furthermore, they are delimiter insensitive, which means that <code>actor.is("a bad person")</code>, <code>actor.is("a_badPERSON")</code> or <code>actor.is.AbadPerson</code> would refer to the same thing.<br><br>
Objects that are direct representations of the in-game objects of Ragnarok(actors, cells, your homunculus/mercenary, your character) have 2 special tables inside each of them. One is called <code>prev</code>, the other <code>last</code>. The first one is used to store information about the object from the previous call of the AI by the client(remember that the data changes only between those calls). The information in the second table changes only when the current data is changed. For example:<br>
</blockquote><ul><li>The script has started and the AI is called for the first time. The current cell of your character is (15,23). The previous cell is <code>nil</code> and the last cell is also <code>nil</code> since there is no previous data available.<br>
</li><li>The second call. Your character does not move. The current cell is (15,23). The previous cell is now also (15,23), since this is the value of the previous call, but the last cell remains <code>nil</code>, because the was no change in the value.<br>
</li><li>The third call. Your character has moved. The current cell is now (16,24). The previous cell remains (15,23), but the last cell changes to (15,23), since the current value has changed and we now know that the last cell, on which our character has stepped was (15,23).<br>
<h3><font color='#006600'>A Few Words About the Syntax</font></h3>
In the description below I use some syntactical aids to reduce the amount of unnecessary repeating text and to make the manual more compact.<br>
For constructors, operators and object methods:<br>
</li><li>I use <font color='#0052A3'>blue</font><b>.<br>
</li><li>After the :: I specify the return type or value of the constructor/method/operator. If the constructor/method/operator can return different types in different situations(for example, <code>nil</code> if something is wrong), then those types are separated with | .<br>
For arguments and object fields:<br>
</li><li>I use</b><font color='#5E5B00'>dark yellow</font><b>for optional arguments(the ones that you can omit when calling a function/method/constructor) and</b><font color='#006666'>cyan</font><b>for mandatory arguments and object fields.<br>
</li><li>If the argument is optional, then I specify the default value(which is used if the argument is omitted) after the | .<br>
</li><li>After the :: I specify the type of the argument/field. If the argument/field can have/contain different types, then those types are separated with | . If the argument is supposed to have not only a certain type, but also I certain value(for example, > 0), then the restriction is specified inside ( ) next to the type.<br>
For strings with specific format:<br>
</li><li>I specify the variable part like so: <code>[partOfTheString]</code>. For example: <code>"abc[num]"</code>, where <code>[num]</code> is a number, would mean that I refer to strings with <code>abc</code> in the beginning and numbers after that, such as: <code>"abc123"</code>, <code>"abc9"</code> or <code>"abc0"</code>.<br>
I also use imaginary types to more specifically identify some return values or arguments:<br>
</li><li><code>sequence</code> - to specify that the function can take an arbitrary number of arguments or return an arbitrary number of values.<br>
</li><li><code>any</code> - to specify that the value can be of any type.<br>
</li><li><code>self</code> - to specify that the method returns the reference to the same object it has been called from. For example,  <code>list.add(2).add(5).remove(1)</code> would add <code>2</code> and <code>5</code> to the list and then remove the 1<sup>st</sup> element from it leaving just 1 element <code>5</code>.<br></b><br>
<hr />
<h3><font color='#006600'>Multipliable Objects</font></h3>
<h4><font color='#660000'>Value</font></h4>
The most primitive object in RAICK. It is used mainly to store the data about <a href='http://code.google.com/p/raick/wiki/Manual#Actor'>actors</a>. Each object consists of a <code>number</code> and a <code>string</code>. In most cases the string is used to describe or translate the meaning of the number(ID), but you can also use the number, for example, to index the string or use only the string without the number. What I am saying is that it is just a <code>string</code>-<code>number</code> pair and it can be interpreted in many ways according to the place or situation it is used in.<br>
Later in this guide I will specify <code>Value</code> objects in the following manner: <code>"string" (number1, number2, ...)</code>. For example:<br>
<ul><li><code>"Assassin" (12)</code> specifies a <code>Value</code> object with <code>"Assassin"</code> for a name and 12 for the number(ID).<br>
</li><li><code>"Attacking" (2, 9)</code> specifies 2 <code>Value</code> objects, both having <code>"Attacking"</code> for a name and 2, 9 for the ID respectively.<br>
In these examples I have specified <code>Value</code> objects that translate original ID's of a character type and an action/motion type into human-readable strings and that is actually the main idea behind this object.<br>
</li></ul></li><li><u><b>Constructors</b></u><br><br>
<ul><li><font color='#0052A3'>Value( <font color='#006666'>name</font> , <font color='#5E5B00'>id</font> )</font><b>:: <code>Value</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>name</b></font> :: <code>string</code><br>
</li></ul><blockquote>Some name.<br>
</blockquote><ul><li><font color='#5E5B00'><b>id</b></font> | <code>0</code> :: <code>number</code><br>
</li></ul><blockquote>Some number, ID or index.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns a new <code>Value</code> object with given <font color='#006666'><b>name</b></font> and <font color='#006666'><b>value</b></font>.<br>
</blockquote></li></ul></li></ul></li><li><u><b>Fields</b></u><br><br>
<ul><li><font color='#006666'><b>name</b></font> :: <code>string</code><br>
</li></ul><blockquote>The name of the value.<br>
</blockquote><ul><li><font color='#006666'><b>id</b></font> :: <code>number</code><br>
</li></ul><blockquote>The ID of the value.<br>
</blockquote></li><li><u><b><i>is</i> Methods</b></u><br><br>
<ul><li><font color='#0052A3'>is( <font color='#006666'>…</font> )</font><b>,</b><font color='#0052A3'>isNot( <font color='#006666'>…</font> )</font><b>:: <code>boolean</code></b><br><br>
<ul><li><b>Accepted Types</b><br><br>
<ul><li><code>Value</code>
</li></ul><blockquote>Returns <code>true</code> if the given value is the same as the current.<br>
</blockquote><ul><li><code>number</code>
</li></ul><blockquote>Returns <code>true</code> if the given number equals the <font color='#006666'><b>id</b></font> of the current object.<br>
</blockquote><ul><li><code>string</code>
</li></ul><blockquote>Returns <code>true</code> if the given string equals the <font color='#006666'><b>name</b></font> of the current object.<br>
</blockquote></li><li><b>Accepted <code>string</code> Values</b> (They are checked if the given string does not equal <font color='#006666'><b>name</b></font>)<br><br>
<ul><li><code>"evolved[HomType]"</code>
</li></ul><blockquote>Returns <code>true</code> if the current object is describing an evolved homunculus of type <code>[HomType]</code>. For example: <code>"evolvedFilir"</code>, <code>"evolvedVanilmirth"</code>.<br>
</blockquote><ul><li><code>"[HomType]Evolved"</code>
</li></ul><blockquote>The same as the previous one, but here <code>evolved</code> is written after the type. For example: <code>"lifEvolved"</code>, <code>"amistrEvolved"</code>.<br>
</blockquote><ul><li><code>"[ScrollLvl][MercType]"</code>
</li></ul><blockquote>Returns <code>true</code> if the current object is describing a mercenary of type <code>[MercType]</code>, which is summoned from scroll of lvl <code>[ScrollLvl]</code>. For example: <code>"6Bowman"</code>, <code>"1fencer"</code>.<br>
</blockquote><ul><li><code>"[MercType][ScrollLvl]"</code>
</li></ul><blockquote>The same as the previous one, except the lvl of the scroll is now in the back. For example: <code>"Lancer10"</code>, <code>"bowman3"</code>.<br>
</blockquote><ul><li><code>"mutated"</code>
</li></ul><blockquote>Returns <code>true</code> if the current object is describing the type of a mutated homunculus i.e. Homunculus S.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>is.<font color='#006666'>value</font></font><b>,</b><font color='#0052A3'>isNot.<font color='#006666'>value</font></font><b>:: <code>boolean</code></b><br>
<hr />
<h4><font color='#660000'>Cell</font></h4>
Represents a cell with (x,y) coordinates on the current map/location. The coordinates of a cell, which your character is currently occupying can always be checked using the <b>/where</b> command.<br>
</li></ul></li><li><u><b>Constructors</b></u><br><br>
<ul><li><font color='#0052A3'>Cell( <font color='#006666'>x</font> , <font color='#006666'>y</font> )</font><b>:: <code>Cell</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>x</b></font> :: <code>number</code> ( > 0 )<br>
</li></ul><blockquote>The X-coordinate of the cell.<br>
</blockquote><ul><li><font color='#006666'><b>y</b></font> :: <code>number</code> ( > 0 )<br>
</li></ul><blockquote>The Y-coordinate of the cell.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns a <code>Cell</code> object with (<font color='#006666'><b>x</b></font>, <font color='#006666'><b>y</b></font>) coordinates.<br>
</blockquote></li></ul></li></ul></li><li><u><b>Fields</b></u><br><br>
<ul><li><font color='#006666'><b>x</b></font> :: <code>number</code><br>
</li></ul><blockquote>The X-coordinate of the cell.<br>
</blockquote><ul><li><font color='#006666'><b>y</b></font> :: <code>number</code><br>
</li></ul><blockquote>The Y-coordinate of the cell.<br>
</blockquote><ul><li><font color='#006666'><b>occupier</b></font> :: <code>Actor</code> | <code>Owner</code> | <code>Homunculus</code> | <code>Mercenary</code> | <code>nil</code><br>
</li></ul><blockquote>The "live" object, which is currently standing on the cell. Contains <code>nil</code> if the cell is empty. In case on multiple occupiers contains only one of them.<br>
</blockquote></li><li><u><b><i>is</i> Methods</b></u><br><br>
<ul><li><font color='#0052A3'>is( <font color='#006666'>…</font> )</font><b>,</b><font color='#0052A3'>isNot( <font color='#006666'>…</font> )</font><b>:: <code>boolean</code></b><br><br>
<ul><li><b>Accepted Types</b><br><br>
<ul><li><code>Cell</code>
</li></ul><blockquote>Returns <code>true</code> if the given cell is the same as the current.<br>
</blockquote></li><li><b>Accepted <code>string</code> Values</b><br><br>
<ul><li><code>"visible"</code>
</li></ul><blockquote>Returns <code>true</code> if the current cell is in range of sight of your character.<br>
</blockquote><ul><li><code>"occupied"</code>
</li></ul><blockquote>Returns <code>true</code> if the current cell is occupied by some actor.<br>
</blockquote><ul><li><code>"[x];[y]"</code>
</li></ul><blockquote>Returns <code>true</code> if the current cell has specified (<code>[x]</code>,<code>[y]</code>) coordinates. The delimiter ; can be replaced with anything you want as long as it is not a number.  For example <code>"23;45"</code>, <code>"23|45"</code>.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>is.<font color='#006666'>value</font></font><b>,</b><font color='#0052A3'>isNot.<font color='#006666'>value</font></font><b>:: <code>boolean</code></b><br><br>
</li></ul></li><li><u><b>Operators</b></u><br><br>
<ul><li><font color='#0052A3'><font color='#006666'>cell</font> + <font color='#006666'>vector</font> <code>*</code> <font color='#5E5B00'>distance</font></font><b>:: <code>Cell</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>cell</b></font> :: <code>Cell</code><br>
</li></ul><blockquote>An arbitrary <code>Cell</code> object.<br>
</blockquote><ul><li><font color='#006666'><b>vector</b></font> :: <code>Vector</code><br>
</li></ul><blockquote>An arbitrary <code>Vector</code> object.<br>
</blockquote><ul><li><font color='#5E5B00'><b>distance</b></font> | <code>1</code> :: <code>number</code><br>
</li></ul><blockquote>The distance, by which the <font color='#006666'>cell</font><b>will be shifted in the direction of</b><font color='#006666'>vector</font><b>. Negative values will shift it in the opposite direction.</b><br>
</blockquote></li><li><b>Description</b>
<blockquote>This equation returns the cell, which is <font color='#5E5B00'>distance</font><b>cells away from the</b><font color='#006666'>cell</font><b>in the direction defined by</b><font color='#006666'>vector</font><b>.<br>
</blockquote></li></ul></li><li></b><font color='#0052A3'><font color='#006666'>cell</font> .. <font color='#006666'>object</font></font><b>:: <code>number</code> | <code>nil</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>cell</b></font> :: <code>Cell</code><br>
</li></ul><blockquote>An arbitrary <code>Cell</code> object.<br>
</blockquote><ul><li><font color='#006666'><b>object</b></font> :: <code>Cell</code> | <code>Actor</code> | <code>Owner</code> |  <code>Homunculus</code> |  <code>Mercenary</code><br>
</li></ul><blockquote>Any in-game object, distance till which you want to know.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns the distance(in cells) between <font color='#006666'><b>cell</b></font> and <font color='#006666'><b>object</b></font> or <code>nil</code> if <font color='#006666'><b>object</b></font> is an actor, which is not visible.<br>
<br>
<hr />
<h4><font color='#660000'>Actor</font></h4>
Represents an in-game character(monster, NPC or player character), which can be distinguished by it's unique ID. <code>Owner</code>, <code>Homunculus</code> and <code>Mercenary</code> objects can also be called actors, but they are allocated into separate objects, since they are <i>special</i> actors(you can get more data about them and send commands to some of them).<br>
</blockquote></li></ul></li></ul></li><li><u><b>Constructors</b></u><br><br>
<ul><li><font color='#0052A3'>Actor( <font color='#5E5B00'>id</font> )</font><b>:: <code>Actor</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#5E5B00'><b>id</b></font> | <code>0</code> :: <code>number</code> ( >= 0 )<br>
</li></ul><blockquote>ID of the actor.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns an <code>Actor</code> object, which represents an in-game character with given ID.<br>
</blockquote></li></ul></li></ul></li><li><u><b>Fields</b></u><br><br>
<ul><li><font color='#006666'><b>id</b></font> :: <code>number</code><br>
</li></ul><blockquote>Actor's ID.<br>
</blockquote><ul><li><font color='#006666'><b>status</b></font> :: <code>Value</code><br>
</li></ul><blockquote>Actor's current visibility status. Can be one of the following:<br><br>
<ul><li><code>"Unknown" (0)</code>
</li></ul><blockquote>The actor is outside of the vision range and the AI cannot get any data about it.<br>
</blockquote><ul><li><code>"Hidden" (1)</code>
</li></ul><blockquote>The actor is inside the vision range, but it is visually hidden(<i>Hiding</i>, <i>Clocking</i> etc), which means that the AI cannot get it's location.<br>
</blockquote><ul><li><code>"Visible" (2)</code>
</li></ul><blockquote>The actor is visually observable.<br>
</blockquote></blockquote><ul><li><font color='#006666'><b>prev.status</b></font> :: <code>Value</code><br>
</li></ul><blockquote>Actor's previous visibility status.<br>
</blockquote><ul><li><font color='#006666'><b>last.status</b></font> :: <code>Value</code><br>
</li></ul><blockquote>Actor's last visibility status.<br>
</blockquote><ul><li><font color='#006666'><b>cell</b></font> :: <code>Cell</code><br>
</li></ul><blockquote>Actor's current cell.<br>
</blockquote><ul><li><font color='#006666'><b>prev.cell</b></font> :: <code>Cell</code><br>
</li></ul><blockquote>Actor's previous cell.<br>
</blockquote><ul><li><font color='#006666'><b>last.cell</b></font> :: <code>Cell</code><br>
</li></ul><blockquote>Actor's last cell.<br>
</blockquote><ul><li><font color='#006666'><b>action</b></font> :: <code>Value</code><br>
</li></ul><blockquote>Actor's current action. Can be one of the following:<br><br>
<ul><li><code>"Unknown" (?)</code>
</li></ul><blockquote>The action is unknown to RAICK.<br>
</blockquote><ul><li><code>"Standing" (0)</code>
</li></ul><blockquote>The actor is standing.<br>
</blockquote><ul><li><code>"Moving" (1)</code>
</li></ul><blockquote>The actor is moving.<br>
</blockquote><ul><li><code>"Attacking" (2, 9)</code>
</li></ul><blockquote>The actor is attacking.<br>
</blockquote><ul><li><code>"Dead" (3)</code>
</li></ul><blockquote>The actor is dead.<br>
</blockquote><ul><li><code>"Damaged" (4)</code>
</li></ul><blockquote>The actor is being damaged.<br>
</blockquote><ul><li><code>"Bending" (5)</code>
</li></ul><blockquote>The actor is bending to place something on the ground or to pick something up.<br>
</blockquote><ul><li><code>"Sitting" (6)</code>
</li></ul><blockquote>The actor is sitting.<br>
</blockquote><ul><li><code>"Casted" (7, 20, 21, 22, 23, 24, 26, 30, 31, 32, 33, 34, 35, 36, 38, 39, 40)</code>
</li></ul><blockquote>The actor has casted/used a skill.<br>
</blockquote><ul><li><code>"Casting" (8, 13, 18, 19, 28, 37, 41, 42)</code>
</li></ul><blockquote>The actor is casting a skill.<br>
</blockquote><ul><li><code>"Throwing" (12)</code>
</li></ul><blockquote>The actor is throwing something.<br>
</blockquote><ul><li><code>"Dancing" (16)</code>
</li></ul><blockquote>The actor is dancing.<br>
</blockquote><ul><li><code>"Performing" (17)</code>
</li></ul><blockquote>The actor is performing a song.<br>
</blockquote></blockquote><ul><li><font color='#006666'><b>prev.action</b></font> :: <code>Value</code><br>
</li></ul><blockquote>Actor's previous action.<br>
</blockquote><ul><li><font color='#006666'><b>last.action</b></font> :: <code>Value</code><br>
</li></ul><blockquote>Actor's last action.<br>
</blockquote><ul><li><font color='#006666'><b>target</b></font> :: <code>Actor</code> | <code>Owner</code> |  <code>Homunculus</code> |  <code>Mercenary</code><br>
</li></ul><blockquote>Actor's current target. Contains a blank actor(<font color='#006666'><b>id</b></font> = 0) if the current actor has no targets. The target is set when you have visually observed that the actor has attacked someone or has started casting any kind of targeted skill. The target is preserved until changed and is reseted(turned to blank actor), when the actor goes beyond your vision range.<br>
</blockquote><ul><li><font color='#006666'><b>prev.target</b></font> :: <code>Actor</code> | <code>Owner</code> |  <code>Homunculus</code> |  <code>Mercenary</code><br>
</li></ul><blockquote>Actor's previous target.<br>
</blockquote><ul><li><font color='#006666'><b>last.target</b></font> :: <code>Actor</code> | <code>Owner</code> |  <code>Homunculus</code> |  <code>Mercenary</code><br>
</li></ul><blockquote>Actor's last target.<br>
</blockquote><ul><li><font color='#006666'><b>group</b></font> :: <code>Value</code><br>
</li></ul><blockquote><i>Note: This field is not defined in the mercenary script, since they cannot distinguish types.</i><br><br>
Actor's type group. Can be one of the following:<br><br>
<ul><li><code>"Unknown" (0)</code>
</li></ul><blockquote>The group is unknown to RAICK.<br>
</blockquote><ul><li><code>"Player" (1)</code>
</li></ul><blockquote>The actor is a player.<br>
</blockquote><ul><li><code>"Mob" (2)</code>
</li></ul><blockquote>The actor is a monster.<br>
</blockquote><ul><li><code>"NPC" (3)</code>
</li></ul><blockquote>The actor is an NPC.<br>
</blockquote><ul><li><code>"Homunculus" (4)</code>
</li></ul><blockquote>The actor is a homunculus.<br>
</blockquote><ul><li><code>"Mercenary" (5)</code>
</li></ul><blockquote>The actor is a mercenary.<br>
</blockquote><ul><li><code>"WoE Stone" (6)</code>
</li></ul><blockquote>The actor is an emperium or any defense stone/barricade in WoE 2.0.<br>
</blockquote><ul><li><code>"WoE Guardian" (7)</code>
</li></ul><blockquote>The actor is a guardian in the castle(not the one in the <i>Thor's Volcano</i>).<br>
</blockquote></blockquote><ul><li><font color='#006666'><b>type</b></font> :: <code>Value</code>
</li></ul><blockquote><i>Note: This field is not defined in the mercenary script, since they cannot distinguish types.</i><br><br>
Actor's type. Can be one of the following depending of the <font color='#006666'><b>group</b></font>:<br><br>
<ul><li><code>"Unknown" (?)</code>
</li></ul><blockquote>The type is unknown to RAICK.<br>
</blockquote><ul><li>For <font color='#006666'><b>group</b></font> <code>"Player"</code>:<br><br>
<ul><li><code>"Novice" (0)</code>
</li><li><code>"Swordman" (1)</code>
</li><li><code>"Magician" (2)</code>
</li><li><code>"Archer" (3)</code>
</li><li><code>"Acolyte" (4)</code>
</li><li><code>"Merchant" (5)</code>
</li><li><code>"Thief" (6)</code>
</li><li><code>"Knight" (7, 13)</code>
</li><li><code>"Priest" (8)</code>
</li><li><code>"Wizard" (9)</code>
</li><li><code>"Blacksmith" (10)</code>
</li><li><code>"Hunter" (11)</code>
</li><li><code>"Assassin" (12)</code>
</li><li><code>"Crusader" (14, 21)</code>
</li><li><code>"Monk" (15)</code>
</li><li><code>"Sage" (16)</code>
</li><li><code>"Rogue" (17)</code>
</li><li><code>"Alchemist" (18)</code>
</li><li><code>"Bard" (19)</code>
</li><li><code>"Dancer" (20)</code>
</li><li><code>"Wedding" (22)</code> - The player is in a wedding dress/tuxedo.<br>
</li><li><code>"Super Novice" (23)</code>
</li><li><code>"Gunslinger" (24)</code>
</li><li><code>"Ninja" (25)</code>
</li><li><code>"Xmas" (26)</code> - The player is wearing the Santa costume.<br>
</li><li><code>"Summer" (27)</code> - The player is wearing the summer beach costume.<br>
</li><li><code>"Novice High" (4001)</code>
</li><li><code>"Swordman High" (4002)</code>
</li><li><code>"Magician High" (4003)</code>
</li><li><code>"Archer High" (4004)</code>
</li><li><code>"Acolyte High" (4005)</code>
</li><li><code>"Merchant High" (4006)</code>
</li><li><code>"Thief High" (4007)</code>
</li><li><code>"Lord Knight" (4008, 4014)</code>
</li><li><code>"High Priest" (4009)</code>
</li><li><code>"High Wizard" (4010)</code>
</li><li><code>"Whitesmith" (4011)</code>
</li><li><code>"Sniper" (4012)</code>
</li><li><code>"Assassin Cross" (4013)</code>
</li><li><code>"Paladin" (4015, 4022)</code>
</li><li><code>"Champion" (4016)</code>
</li><li><code>"Professor" (4017)</code>
</li><li><code>"Stalker" (4018)</code>
</li><li><code>"Creator" (4019)</code>
</li><li><code>"Clown" (4020)</code>
</li><li><code>"Gypsy" (4021)</code>
</li><li><code>"Baby Novice" (4023)</code>
</li><li><code>"Baby Swordman" (4024)</code>
</li><li><code>"Baby Magician" (4025)</code>
</li><li><code>"Baby Archer" (4026)</code>
</li><li><code>"Baby Acolyte" (4027)</code>
</li><li><code>"Baby Merchant" (4028)</code>
</li><li><code>"Baby Thief" (4029)</code>
</li><li><code>"Baby Knight" (4030, 4036)</code>
</li><li><code>"Baby Priest" (4031)</code>
</li><li><code>"Baby Wizard" (4032)</code>
</li><li><code>"Baby Blacksmith" (4033)</code>
</li><li><code>"Baby Hunter" (4034)</code>
</li><li><code>"Baby Assassin" (4035)</code>
</li><li><code>"Baby Crusader" (4037, 4044)</code>
</li><li><code>"Baby Monk" (4038)</code>
</li><li><code>"Baby Sage" (4039)</code>
</li><li><code>"Baby Rogue" (400)</code>
</li><li><code>"Baby Alchemist" (4041)</code>
</li><li><code>"Baby Bard" (4042)</code>
</li><li><code>"Baby Dancer" (4043)</code>
</li><li><code>"Super Baby" (4045)</code>
</li><li><code>"Taekwon" (4046)</code>
</li><li><code>"Star Gladiator" (4047, 4048)</code>
</li><li><code>"Soul Linker" (4049)</code>
</li><li><code>"Gangsi" (4050)</code>
</li><li><code>"Death Knight" (4051)</code>
</li><li><code>"Dark Collector" (4052)</code>
</li><li><code>"Rune Knight" (4054, 4060, 4080, 4081)</code>
</li><li><code>"Warlock" (4055, 4061)</code>
</li><li><code>"Ranger" (4056, 4062, 4084, 4085)</code>
</li><li><code>"Arch Bishop" (4057, 4063)</code>
</li><li><code>"Mechanic" (4058, 4064, 4086, 4087)</code>
</li><li><code>"Guillotine Cross" (4059, 4065)</code>
</li><li><code>"Royal Guard" (4066, 4073, 4082, 4083)</code>
</li><li><code>"Sorcerer" (4067, 4074)</code>
</li><li><code>"Minstrel" (4068, 4075, 4069, 4076)</code>
</li><li><code>"Sura" (4070, 4077)</code>
</li><li><code>"Genetic" (4071, 4078)</code>
</li><li><code>"Shadow Chaser" (4072, 4079)</code>
</li><li><code>"Baby Rune Knight" (4096, 4109)</code>
</li><li><code>"Baby Warlock" (4097)</code>
</li><li><code>"Baby Ranger" (4098, 4111)</code>
</li><li><code>"Baby Arch Bishop" (4099)</code>
</li><li><code>"Baby Mechanic" (4100, 4112)</code>
</li><li><code>"Baby Guillotine Cross" (4101)</code>
</li><li><code>"Baby Royal Guard" (4102, 4110)</code>
</li><li><code>"Baby Sorcerer" (4103)</code>
</li><li><code>"Baby Minstrel" (4104)</code>
</li><li><code>"Baby Wanderer" (4105)</code>
</li><li><code>"Baby Sura" (4106)</code>
</li><li><code>"Baby Genetic" (4107)</code>
</li><li><code>"Baby Shadow Chaser" (4108)</code>
</li><li><code>"Super Novice Ex" (4190)</code>
</li><li><code>"Super Baby Ex" (4191)</code>
</li><li><code>"Kagerou" (4211)</code>
</li><li><code>"Oboro" (4212)</code><br><br>
</li></ul></li><li>For <font color='#006666'><b>group</b></font> <code>"Mob"</code>:<br>
</li></ul><blockquote>RAICK knows the names of pretty much every monster. The list is kept as up-to-date as possible. The names are identical to those used in the game, except for <i>Incarnation of Morroc</i> mobs. Their names have been changed, so they could be distinguished from one another:<br><br>
<ul><li><code>"Morroc Winged" (1918, 1922)</code>
</li></ul><blockquote>The winged one.<br>
</blockquote><ul><li><code>"Morroc Golem" (1919, 1923)</code>
</li></ul><blockquote>The muddy one.<br>
</blockquote><ul><li><code>"Morroc Zombie" (1920, 1924)</code>
</li></ul><blockquote>The up-side-down zombie.<br>
</blockquote><ul><li><code>"Morroc Ghost" (1921, 1925)</code>
</li></ul><blockquote>The ghost.<br>
</blockquote>If the mob has twin names like <i>Desert Wolf Baby</i> / <i>Baby Desert Wolf</i>, then use the one that is written on it's card. If you still have doubts about what name stands for what ID you can find the full list of ID-name pairs somewhere at line 800 in the <code>RAICK.lua</code> file.<br>
</blockquote><ul><li>For <font color='#006666'><b>group</b></font> <code>"NPC"</code>:<br><br>
<ul><li><code>"Kafra" (112, 113, 114, 115, 116, 117, 423, 721, 791, 859, 860, 861)</code>
</li></ul><blockquote>Kafra NPC.<br>
</blockquote><ul><li><code>"Warp" (45)</code>
</li></ul><blockquote>The portal between locations/maps(not the one from the <i>Warp Portal</i> skill).<br>
</blockquote><ul><li><code>"Castle Flag" (111)</code>
</li></ul><blockquote>The flag used in WoE 2.0 by the defending guild to teleport to different locations of the castle.<br>
</blockquote><ul><li><code>"Guild Flag" (772)</code>
</li></ul><blockquote>The castle flag containing the emblem of the guild.<br>
</blockquote></li><li>For <font color='#006666'><b>group</b></font> <code>"Homunculus"</code>:<br><br>
<ul><li><code>"Lif" (6001, 6005, 6009, 6013)</code>
</li><li><code>"Amistr" (6002, 6006, 6010, 6014)</code>
</li><li><code>"Filir" (6003, 6007, 6011, 6015)</code>
</li><li><code>"Vanilmirth" (6004, 6008, 6012, 6016)</code>
</li><li><code>"Eira" (6048)</code>
</li><li><code>"Bayeri" (6049)</code>
</li><li><code>"Sera" (6050)</code>
</li><li><code>"Dieter" (6051)</code>
</li><li><code>"Eleanor" (6052)</code><br><br>
</li></ul></li><li>For <font color='#006666'><b>group</b></font> <code>"Mercenary"</code>:<br><br>
<ul><li><code>"Bowman" (6017, 6018, 6019, 6020, 6021, 6022, 6023, 6024, 6025, 6026)</code>
</li><li><code>"Lancer" (6027, 6028, 6029, 6030, 6031, 6032, 6033, 6034, 6035, 6036)</code>
</li><li><code>"Fencer" (6037, 6038, 6039, 6040, 6041, 6042, 6043, 6044, 6045, 6046)</code>
</li><li><code>"Mimic" (1191)</code>
</li><li><code>"Disguise" (1506)</code>
</li><li><code>"Alice" (1275)</code>
</li><li><code>"Wild Rose" (1965)</code>
</li><li><code>"Doppelganger" (1966)</code>
</li><li><code>"Egnigem Cenia" (1967)</code>
</li><li><code>"Game Master" (2000, 2001)</code>
</li><li><code>"Valkyrie Randgris" (2037, 2038)</code><br><br>
</li></ul></li><li>For <font color='#006666'><b>group</b></font> <code>"WoE Stone"</code>:<br><br>
<ul><li><code>"Emperium" (1288)</code>
</li><li><code>"Barricade" (1905, 1906)</code>
</li><li><code>"Stone" (1907, 1908)</code><br><br>
</li></ul></li><li>For <font color='#006666'><b>group</b></font> <code>"WoE Guardian"</code>:<br><br>
<ul><li><code>"WoE1 Swordman" (1286, 1287)</code>
</li><li><code>"WoE1 Archer" (1285)</code>
</li><li><code>"WoE2 Swordman" (1899)</code>
</li><li><code>"WoE2 Archer" (1900)</code><br><br>
</li></ul></li></ul></blockquote><ul><li><font color='#006666'><b>vector</b></font> :: <code>Vector</code><br>
</li></ul><blockquote>Actor's current motion vector. This vector reflects the current movement direction of the actor. More about vectors <a href='http://code.google.com/p/raick/wiki/Manual#Vector'>here</a>.<br>
</blockquote><ul><li><font color='#006666'><b>prev.vector</b></font> :: <code>Vector</code><br>
</li></ul><blockquote>Actor's previous motion vector.<br>
</blockquote><ul><li><font color='#006666'><b>last.vector</b></font> :: <code>Vector</code><br>
</li></ul><blockquote>Actor's last motion vector.<br>
</blockquote></li><li><u><b><i>is</i> Methods</b></u><br><br>
<ul><li><font color='#0052A3'>is( <font color='#006666'>…</font> )</font><b>,</b><font color='#0052A3'>isNot( <font color='#006666'>…</font> )</font><b>:: <code>boolean</code></b><br><br>
<ul><li><b>Accepted Types</b><br><br>
<ul><li><code>Actor</code>
</li></ul><blockquote>Returns <code>true</code> if the given actor is the same as the current.<br>
</blockquote><ul><li><code>number</code>
</li></ul><blockquote>Returns <code>true</code> if the current actor has the same ID.<br>
</blockquote></li><li><b>Accepted <code>string</code> Values</b><br><br>
<ul><li><code>"[id]"</code>
</li></ul><blockquote>Returns <code>true</code> if the current actor's ID equals <code>[id]</code>.<br>
</blockquote><ul><li><code>"player"</code>
</li></ul><blockquote>Returns <code>true</code> if the current actor is a player character.<br>
</blockquote><ul><li><code>"mob"</code>
</li></ul><blockquote>Returns <code>true</code> if the current actor is a monster.<br>
</blockquote><ul><li><code>"blank"</code>
</li></ul><blockquote>Returns <code>true</code> if the current actor is a blank actor(<font color='#006666'><b>id</b></font> = 0).<br>
</blockquote></li></ul></li><li><font color='#0052A3'>is.<font color='#006666'>value</font></font><b>,</b><font color='#0052A3'>isNot.<font color='#006666'>value</font></font><b>:: <code>boolean</code></b><br><br>
</li></ul></li><li><u><b>Operators</b></u><br><br>
<ul><li><font color='#0052A3'><font color='#006666'>actor</font> .. <font color='#006666'>object</font></font><b>:: <code>number</code> | <code>nil</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>actor</b></font> :: <code>Actor</code><br>
</li></ul><blockquote>An arbitrary <code>Actor</code> object.<br>
</blockquote><ul><li><font color='#006666'><b>object</b></font> :: <code>Cell</code> | <code>Actor</code> | <code>Owner</code> |  <code>Homunculus</code> |  <code>Mercenary</code><br>
</li></ul><blockquote>Any in-game object, distance till which you want to know.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns the distance(in cells) between <font color='#006666'><b>actor</b></font> and <font color='#006666'><b>object</b></font> or <code>nil</code> if at least one of them is not visible.<br>
<br>
<hr />
<h4><font color='#660000'>Points</font></h4>
Represents your or your bot's HP or SP. It is very similar to the <code>Value</code> object, but has some extra fields and <code>is</code> method functionality allowing you to easily get all the information you need about those values.<br>
</blockquote></li></ul></li></ul></li><li><u><b>Constructors</b></u><br><br>
<ul><li><font color='#0052A3'>Points( <font color='#006666'>current</font> , <font color='#006666'>max</font> )</font><b>:: <code>Points</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>current</b></font> :: <code>number</code><br>
</li></ul><blockquote>The current value of HP or SP(depending on what the object represents).<br>
</blockquote><ul><li><font color='#006666'><b>max</b></font> :: <code>number</code><br>
</li></ul><blockquote>The maximum value of HP or SP.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns a new <code>Points</code> object with given current and maximum values. This objects will represent the state of the HP or SP in the given moment of time. Normally, you would not need to create any of these objects yourself, but the constructor is still available incase you can think of a way to use this object for your own purposes.<br>
</blockquote></li></ul></li></ul></li><li><u><b>Fields</b></u><br><br>
<ul><li><font color='#006666'><b>current</b></font> :: <code>number</code><br>
</li></ul><blockquote>The current value of HP or SP.<br>
</blockquote><ul><li><font color='#006666'><b>max</b></font> :: <code>number</code><br>
</li></ul><blockquote>The maximum value of HP or SP.<br>
</blockquote><ul><li><font color='#006666'><b>percent</b></font> :: <code>number</code><br>
</li></ul><blockquote>The current percent value of HP or SP.<br>
</blockquote></li><li><u><b><i>is</i> Methods</b></u><br><br>
<ul><li><font color='#0052A3'>is( <font color='#006666'>…</font> )</font><b>,</b><font color='#0052A3'>isNot( <font color='#006666'>…</font> )</font><b>:: <code>boolean</code></b><br><br>
<ul><li><b>Accepted Types</b><br><br>
<ul><li><code>Points</code>
</li></ul><blockquote>Returns <code>true</code> if the given object has the same <font color='#006666'><b>current</b></font> and <font color='#006666'><b>max</b></font> field values as the current one.<br>
</blockquote><ul><li><code>number</code>
</li></ul><blockquote>Returns <code>true</code> if the given number equals the <font color='#006666'><b>current</b></font> field value of the current object.<br>
</blockquote></li><li><b>Accepted <code>string</code> Values</b><br><br>
<ul><li><code>"full"</code>
</li></ul><blockquote>Returns <code>true</code> if current object's <font color='#006666'><b>current</b></font> value equals <font color='#006666'><b>max</b></font>.<br>
</blockquote><ul><li><code>"[Operator][Current]"</code>
</li></ul><blockquote>Returns <code>true</code> if current object's <font color='#006666'><b>current</b></font> value fits the condition given inside the string. The <code>[Current]</code> is the value of the <font color='#006666'><b>current</b></font> field and the <code>[Operator]</code> can be: <code>=</code>, <code>==</code>, <code>&gt;</code>, <code>&lt;</code>, <code>&gt;=</code>, <code>&lt;=</code> or not specified at all(which is the same as <code>=</code>, <code>==</code>). The meaning is straightforward, for example: <code>"1456"</code>, <code>"= 1456"</code> or <code>"==1456"</code> would all mean <i>current value equals 1456</i> and <code>"&gt;1378"</code> would mean <i>current value is larger, than 1378</i>. You can also put spaces between the operator and the value as shown above with <code>"= 1456"</code>.<br>
</blockquote><ul><li><code>"[Operator][Percent]%"</code>
</li></ul><blockquote>The same as previous one, but checks the <font color='#006666'><b>percent</b></font> field. For example: <code>"56.7%"</code>, <code>"&lt; 100%"</code>, <code>"&gt;=10.134323%"</code>.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>is.<font color='#006666'>value</font></font><b>,</b><font color='#0052A3'>isNot.<font color='#006666'>value</font></font><b>:: <code>boolean</code></b><br>
<hr />
<h4><font color='#660000'>Skill</font></h4>
Represents the skills that your bot can use. It is used either to get information about the skill or to order your bot to use it. Although this object has a constructor you would not normally need to use it, because every skill object available can be accessed by it's name. For example, if you query variables: <code>Devotion</code>, <code>TouchOfHeal</code>, <code>SBR44</code>, <code>MentalChange</code> they would all contain skill objects for those skills(i.e. querying <code>Skill(8013)</code> has the same effect as querying variable <code>Caprise</code>). RAICK even knows the synonyms and some shorter versions used by players: <code>Sacrifice</code>, <code>HealingHands</code>, <code>SBR</code>, <code>Mental</code>.<br>
If you're not sure what names of skills does RAICK understand, then just open the <code>RAICK.lua</code> file and somewhere at line 2400 you will find a long list of skill definitions with skill names as the first line of every definition.<br>
<br>
All names are case and delimiter insensitive, which means that your can write <code>S_B_R</code> or <code>healing_HAND_S</code> and you would still get your objects.<br>
</li></ul></li><li><u><b>Constructors</b></u><br><br>
<ul><li><font color='#0052A3'>Skill( <font color='#006666'>id</font> )</font><b>:: <code>Skill</code> | <code>nil</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>id</b></font> :: <code>number</code><br>
</li></ul><blockquote>The ID of the skill.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns the <code>Skills</code> object representing the skill with the given ID or <code>nil</code> if no such skill exist or if this skill cannot be used by the current homunculus/mercenary or its currently active <i>cobot</i>(see <a href='http://code.google.com/p/raick/wiki/Manual#Data_Exchange_Between_Homunculus_and_Mercenary'>Data Exchange Between Homunculus and Mercenary</a>). The last fact is also true when you query skill objects by their names through variables. For example, variable <code>Caprise</code> would contain <code>nil</code> for <code>Amistr</code> and the corresponding object for <code>Vanilmirth</code>. This makes it easy to check if the current user of the script has the corresponding skill like so:<br>
<pre><code><br>
if Caprise then<br>
-- ...<br>
</code></pre>
However, this will not work for normal homunculus skills when the user of the script is a mutated homunculus(Homunculus S), since potentially they can have access to every skill of normal homunculi and therefore all skills of normal homunculi are defined for them in the script.<br>
</blockquote></li></ul></li></ul></li><li><u><b>Fields</b></u><br><br>
<ul><li><font color='#006666'><b>id</b></font> :: <code>number</code><br>
</li></ul><blockquote>The ID of the skill.<br>
</blockquote><ul><li><font color='#006666'><b>name</b></font> :: <code>string</code><br>
</li></ul><blockquote>The name of the skill.<br>
</blockquote><ul><li><font color='#006666'><b>maxLevel</b></font> :: <code>number</code><br>
</li></ul><blockquote>The maximum level of the skill.<br>
</blockquote><ul><li><font color='#006666'><b>range</b></font> :: <code>number</code> | <code>nil</code><br>
</li></ul><blockquote>The range of the skill. Contains the maximum distance from the owner for skill to be usable in case of homunculus supportive skills like <i>Urgent Escape</i>. <code>nil</code> if the skill does not have any range restrictions.<br>
</blockquote><ul><li><font color='#006666'><b>range<code>[</code>lvl<code>]</code></b></font> :: <code>number</code> | <code>nil</code><br>
</li></ul><blockquote>This is a special syntax to get ranges of some Homunculus S skills, whose range depends on level of the skill. <code>[lvl]</code> can be between 1 and 4(e.g. <code>range3</code>, <code>range1</code>). The standard <code>range</code> field in case of those skills contains the maximum range i.e. range for the 5<sup>th</sup> level.<br>
</blockquote></li><li><u><b>Methods</b></u><br><br>
<ul><li><font color='#0052A3'>sp( <font color='#5E5B00'>lvl</font> )</font><b>:: <code>number</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#5E5B00'><b>lvl</b></font> | <font color='#006666'><b>maxLevel</b></font> :: <code>number</code><br>
</li></ul><blockquote>The level of the skill.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns the amount SP needed to use the current skill of specified level.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>duration( <font color='#5E5B00'>lvl</font> )</font><b>:: <code>number</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#5E5B00'><b>lvl</b></font> | <font color='#006666'><b>maxLevel</b></font> :: <code>number</code><br>
</li></ul><blockquote>The level of the skill.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns the duration of effect in milliseconds for the current skill of specified level. Returns 0 if the skill does not have a duration.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>delay( <font color='#5E5B00'>lvl</font> )</font><b>:: <code>number</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#5E5B00'><b>lvl</b></font> | <font color='#006666'><b>maxLevel</b></font> :: <code>number</code><br>
</li></ul><blockquote>The level of the skill.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns the delay in milliseconds for the current skill of specified level. Returns 0 if the skill does not have a delay.<br>
<br>
<hr />
<h4><font color='#660000'>List</font></h4>
A simple list for storing multiple values and manipulating them.<br>
</blockquote></li></ul></li></ul></li><li><u><b>Constructors</b></u><br><br>
<ul><li><font color='#0052A3'>List( <font color='#5E5B00'>…</font> )</font><b>:: <code>List</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#5E5B00'><b>…</b></font> :: <code>sequence</code><br>
</li></ul><blockquote>A sequence of values of any type.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns a new <code>List</code> object containing the specified values or an empty list if no values are given.<br>
</blockquote></li></ul></li></ul></li><li><u><b>Fields</b></u><br><br>
<ul><li><font color='#006666'><b>size</b></font> :: <code>number</code><br>
</li></ul><blockquote>The number of elements in the list.<br>
</blockquote></li><li><u><b>Methods</b></u><br><br>
<ul><li><font color='#0052A3'>clear()</font><b>:: <code>self</code></b><br>
</li></ul><blockquote>Clears the list.<br>
</blockquote><ul><li><font color='#0052A3'>clone()</font><b>:: <code>List</code></b><br>
</li></ul><blockquote>Returns a copy of the list.<br>
</blockquote><ul><li><font color='#0052A3'>each()</font><b>:: <code>function</code></b><br>
</li></ul><blockquote>Returns an <i>iteration function</i> for the current list. All you need to know about this function is that it is  used to go through the list using the <code>for</code> loop like so:<br>
<pre><code><br>
for index, value in list.each() do<br>
end<br>
</code></pre>
</blockquote><ul><li><font color='#0052A3'>elements()</font><b>:: <code>sequence</code></b><br>
</li></ul><blockquote>Returns the content of the list as a sequence of elements(as if the values were written one after another with commas between them).<br>
</blockquote><ul><li><font color='#0052A3'>get( <font color='#5E5B00'>n</font> )</font><b>:: <code>any</code> | <code>nil</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#5E5B00'><b>n</b></font> | <font color='#006666'><b>size</b></font> :: <code>number</code><br>
</li></ul><blockquote>The number of the element.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns the <font color='#5E5B00'><b>n</b></font>'th element of the list or the last one if <font color='#5E5B00'><b>n</b></font> is omitted or <code>nil</code> if the list is empty.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>add( <font color='#006666'>v</font> )</font><b>:: <code>self</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>v</b></font> :: <code>any</code><br>
</li></ul><blockquote>The value that needs to be added.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Adds the given value to the list.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>put( <font color='#006666'>n</font> , <font color='#006666'>v</font> )</font><b>:: <code>self</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>n</b></font> :: <code>number</code><br>
</li></ul><blockquote>The index of the element in the list.<br>
</blockquote><ul><li><font color='#006666'><b>v</b></font> :: <code>any</code><br>
</li></ul><blockquote>The replacement value.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Replaces the value under the index <font color='#006666'><b>n</b></font> with <font color='#006666'><b>v</b></font>. Does nothing if the specified index is empty.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>addList( <font color='#006666'>l</font> )</font><b>:: <code>self</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>l</b></font> :: <code>List</code><br>
</li></ul><blockquote>The list of values that need to be added.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Adds all elements of the given list to the current list.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>mergeList( <font color='#006666'>l</font> )</font><b>:: <code>self</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>l</b></font> :: <code>List</code><br>
</li></ul><blockquote>The list of values that need to be merged with the current one.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Adds only those elements of <font color='#006666'><b>l</b></font> that don't exist in the current list.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>remove( <font color='#5E5B00'>n</font> )</font><b>:: <code>self</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#5E5B00'><b>n</b></font> | <font color='#006666'><b>size</b></font> :: <code>number</code><br>
</li></ul><blockquote>The number of the element.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Removes the <font color='#5E5B00'><b>n</b></font>'th element from the list or the last one if <font color='#5E5B00'><b>n</b></font> is omitted or does nothing if the list is empty.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>removeList( <font color='#006666'>l</font> )</font><b>:: <code>self</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>l</b></font> :: <code>List</code><br>
</li></ul><blockquote>The list of values that need to be removes from the current list.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Removes all elements from the current list that exist in <font color='#006666'><b>l</b></font>.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>removeAll( <font color='#006666'>v</font> )</font><b>:: <code>self</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>v</b></font> :: <code>any</code><br>
</li></ul><blockquote>The value that needs to be removed from the list.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Removes all encounters(if there are many identical values) of <font color='#006666'><b>v</b></font>.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>contains( <font color='#006666'>v</font> )</font><b>:: <code>boolean</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>v</b></font> :: <code>any</code><br>
</li></ul><blockquote>An arbitrary value.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns <code>true</code> if the current list contains the given value.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>containsList( <font color='#006666'>l</font> )</font><b>:: <code>boolean</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>l</b></font> :: <code>List</code><br>
</li></ul><blockquote>An arbitrary list.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns <code>true</code> if the current list contains all values of the given list.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>closestTo( <font color='#006666'>v</font> )</font><b>:: <code>Cell</code> | <code>Actor</code> | <code>Owner</code> |  <code>Homunculus</code> |  <code>Mercenary</code> | <code>nil</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>v</b></font> :: <code>Cell</code> | <code>Actor</code> | <code>Owner</code> |  <code>Homunculus</code> |  <code>Mercenary</code><br>
</li></ul><blockquote>A location or an in-game character.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Looks through all objects of the current list, between which the distance can be calculated and returns the closest object to <font color='#006666'><b>v</b></font> or <code>nil</code> if the list does not contain any objects of that kind.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>farthestFrom( <font color='#006666'>v</font> )</font><b>:: <code>Cell</code> | <code>Actor</code> | <code>Owner</code> |  <code>Homunculus</code> |  <code>Mercenary</code> | <code>nil</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>v</b></font> :: <code>Cell</code> | <code>Actor</code> | <code>Owner</code> |  <code>Homunculus</code> |  <code>Mercenary</code><br>
</li></ul><blockquote>A location or an in-game character.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Looks through all objects of the current list, between which the distance can be calculated and returns the farthest object from <font color='#006666'><b>v</b></font> or <code>nil</code> if the list does not contain any objects of that kind.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>filter( <font color='#006666'>f</font> )</font><b>:: <code>List</code>
<ul><li></b>Arguments<br><br>
<ul><li><font color='#006666'><b>f</b></font> :: <code>function</code><br>
</li></ul><blockquote>The filtering function.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns a new list containing only the values approved by the given filter. Allows filtering out certain data without the use of loops. The filtering function receives one argument and must return <code>true</code> if the value is approved and <code>false</code> otherwise. For example:<br>
<pre><code><br>
list = List(1,2,3)<br>
<br>
function    filter(value)<br>
<br>
if value &gt; 1 then<br>
return true<br>
else<br>
return false<br>
end<br>
end<br>
<br>
filteredList = list.filter(filter) -- 'filteredList' contains values 2 and 3<br>
</code></pre>
You can define filters in the <code>On Startup</code> file.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>filterOne( <font color='#006666'>f</font> )</font><b>:: <code>any</code>
<ul><li></b>Arguments<br><br>
<ul><li><font color='#006666'><b>f</b></font> :: <code>function</code><br>
</li></ul><blockquote>The filtering function.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns the first value that is approved by the given filter.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>forEach( <font color='#006666'>f</font> )</font><b>:: <code>Map</code>
<ul><li></b>Arguments<br><br>
<ul><li><font color='#006666'><b>f</b></font> :: <code>function</code><br>
</li></ul><blockquote>The transformation function.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns a map, where results of applying <font color='#006666'><b>f</b></font> for each element of the list are stored under those elements(elements of the list are <i>keys</i> and the corresponding transformation results are <i>values</i>). The transformation function receives one argument and must return any value, which will be the result of the transformation.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>removeFirst( <font color='#006666'>v</font> , <font color='#5E5B00'>n</font> )</font><b>:: <code>self</code>
<ul><li></b>Arguments<br><br>
<ul><li><font color='#006666'><b>v</b></font> :: <code>any</code><br>
</li></ul><blockquote>The value that is removed.<br>
</blockquote><ul><li><font color='#5E5B00'><b>n</b></font> | <code>1</code> :: <code>number</code><br>
</li></ul><blockquote>The number of removes.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Removes <font color='#5E5B00'><b>n</b></font> occurrences of <font color='#006666'><b>v</b></font> starting from the beginning of the list.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>removeLast( <font color='#006666'>v</font> , <font color='#5E5B00'>n</font> )</font><b>:: <code>self</code>
<ul><li></b>Arguments<br><br>
<ul><li><font color='#006666'><b>v</b></font> :: <code>any</code><br>
</li></ul><blockquote>The value that is removed.<br>
</blockquote><ul><li><font color='#5E5B00'><b>n</b></font> | <code>1</code> :: <code>number</code><br>
</li></ul><blockquote>The number of removes.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Removes <font color='#5E5B00'><b>n</b></font> occurrences of <font color='#006666'><b>v</b></font> starting from the back of the list.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>replace( <font color='#006666'>v</font> , <font color='#5E5B00'>n</font> )</font><b>:: <code>self</code>
<ul><li></b>Arguments<br><br>
<ul><li><font color='#006666'><b>v</b></font> :: <code>any</code><br>
</li></ul><blockquote>The replacement value.<br>
</blockquote><ul><li><font color='#5E5B00'><b>n</b></font> | <font color='#006666'><b>size</b></font> :: <code>number</code><br>
</li></ul><blockquote>The number of the element.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Replaces the <font color='#5E5B00'><b>n</b></font>'th value of the list with <font color='#006666'><b>v</b></font>.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>replaceAll( <font color='#006666'>v1</font> , <font color='#006666'>v2</font> )</font><b>:: <code>self</code>
<ul><li></b>Arguments<br><br>
<ul><li><font color='#006666'><b>v1</b></font> :: <code>any</code><br>
</li></ul><blockquote>The value that is replaced.<br>
</blockquote><ul><li><font color='#006666'><b>v2</b></font> :: <code>any</code><br>
</li></ul><blockquote>The replacement value for <font color='#006666'><b>v1</b></font>.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Replaces all occurrences of <font color='#006666'><b>v1</b></font> with <font color='#006666'><b>v2</b></font>.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>replaceFirst( <font color='#006666'>v1</font> , <font color='#006666'>v2</font> , <font color='#5E5B00'>n</font> )</font><b>:: <code>self</code>
<ul><li></b>Arguments<br><br>
<ul><li><font color='#006666'><b>v1</b></font> :: <code>any</code><br>
</li></ul><blockquote>The value that is replaced.<br>
</blockquote><ul><li><font color='#006666'><b>v2</b></font> :: <code>any</code><br>
</li></ul><blockquote>The replacement value for <font color='#006666'><b>v1</b></font>.<br>
</blockquote><ul><li><font color='#5E5B00'><b>n</b></font> | <code>1</code> :: <code>number</code><br>
</li></ul><blockquote>The number of replacements.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Replaces <font color='#5E5B00'><b>n</b></font> occurrences of <font color='#006666'><b>v1</b></font> with <font color='#006666'><b>v2</b></font> starting from the beginning of the list.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>replaceLast( <font color='#006666'>v1</font> , <font color='#006666'>v2</font> , <font color='#5E5B00'>n</font> )</font><b>:: <code>self</code>
<ul><li></b>Arguments<br><br>
<ul><li><font color='#006666'><b>v1</b></font> :: <code>any</code><br>
</li></ul><blockquote>The value that is replaced.<br>
</blockquote><ul><li><font color='#006666'><b>v2</b></font> :: <code>any</code><br>
</li></ul><blockquote>The replacement value for <font color='#006666'><b>v1</b></font>.<br>
</blockquote><ul><li><font color='#5E5B00'><b>n</b></font> | <code>1</code> :: <code>number</code><br>
</li></ul><blockquote>The number of replacements.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Replaces <font color='#5E5B00'><b>n</b></font> occurrences of <font color='#006666'><b>v1</b></font> with <font color='#006666'><b>v2</b></font> starting from the back of the list.<br>
<br>
</blockquote></li></ul></li></ul></li><li><u><b><i>is</i> Methods</b></u><br><br>
<ul><li><font color='#0052A3'>is( <font color='#006666'>…</font> )</font><b>,</b><font color='#0052A3'>isNot( <font color='#006666'>…</font> )</font><b>:: <code>boolean</code></b><br><br>
<ul><li><b>Accepted Types</b><br><br>
<ul><li><code>List</code>
</li></ul><blockquote>Returns <code>true</code> if the given list contains the same elements(order does not count).<br>
</blockquote></li><li><b>Accepted <code>string</code> Values</b><br><br>
<ul><li><code>"empty"</code>
</li></ul><blockquote>Returns <code>true</code> if the current list is empty.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>is.<font color='#006666'>value</font></font><b>,</b><font color='#0052A3'>isNot.<font color='#006666'>value</font></font><b>:: <code>boolean</code></b><br><br>
<hr />
<h4><font color='#660000'>Map</font></h4>
Basically, an advanced version of the <code>table</code>. It's main advantage is that unlike the <code>table</code> it can be saved to memory. The map can be accessed either through methods: <code>map.put("a",1)</code>, <code>map.get("a")</code> or like an ordinary <code>table</code>: <code>map["a"] = 1</code>, <code>map["a"]</code>, <code>map.a = 1</code>, <code>map.a</code>. Just remember that using square brackets you cannot query values stored under string keys that are identical to method names.<br>
</li></ul></li><li><u><b>Constructors</b></u><br><br>
<ul><li><font color='#0052A3'>Map( <font color='#5E5B00'>…</font> )</font><b>:: <code>Map</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#5E5B00'><b>…</b></font> :: <code>sequence</code> ( must not contain <code>nil</code>'s for odd elements )<br>
</li></ul><blockquote>A sequence of values of any type with an even number of elements. If the number is odd, then the last element is not counted.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns a new <code>Map</code> object containing the specified key-value pairs or an empty map if the number of given values is less than 2.<br>
</blockquote></li></ul></li></ul></li><li><u><b>Fields</b></u><br><br>
<ul><li><font color='#006666'><b>size</b></font> :: <code>number</code><br>
</li></ul><blockquote>The number of elements in the map.<br>
</blockquote></li><li><u><b>Methods</b></u><br><br>
<ul><li><font color='#0052A3'>clear()</font><b>:: <code>self</code></b><br>
</li></ul><blockquote>Clears the map.<br>
</blockquote><ul><li><font color='#0052A3'>clone()</font><b>:: <code>Map</code></b><br>
</li></ul><blockquote>Returns a copy of the map.<br>
</blockquote><ul><li><font color='#0052A3'>each()</font><b>:: <code>function</code></b><br>
</li></ul><blockquote>Returns an <i>iteration function</i> for the current map. All you need to know about this function is that it is used to go through the map using the <code>for</code> loop like so:<br>
<pre><code><br>
for index, key, value in map.each() do<br>
end<br>
</code></pre>
</blockquote><ul><li><font color='#0052A3'>keys()</font><b>:: <code>List</code></b><br><br>
</li></ul><blockquote>Returns all key values of the map.<br>
</blockquote><ul><li><font color='#0052A3'>values()</font><b>:: <code>List</code></b><br><br>
</li></ul><blockquote>Returns all distinct values of the map.<br>
</blockquote><ul><li><font color='#0052A3'>get( <font color='#006666'>k</font> )</font><b>:: <code>any</code> | <code>nil</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>k</b></font> :: <code>any</code> ( except <code>nil</code> )<br>
</li></ul><blockquote>The key of the map.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns the value stored under the given key or <code>nil</code> if this key is empty.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>put( <font color='#006666'>k</font> , <font color='#006666'>v</font> )</font><b>:: <code>self</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>k</b></font> :: <code>any</code> ( except <code>nil</code> )<br>
</li></ul><blockquote>The key of the map.<br>
</blockquote><ul><li><font color='#006666'><b>v</b></font> :: <code>any</code><br>
</li></ul><blockquote>The value that is placed under key <font color='#006666'><b>k</b></font>.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Put the given value under the given key.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>contains( <font color='#006666'>k</font> )</font><b>:: <code>boolean</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>k</b></font> :: <code>any</code><br>
</li></ul><blockquote>The key of the map.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns <code>true</code> if the given key has a value stored under it.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>containsValue( <font color='#006666'>v</font> )</font><b>:: <code>boolean</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>v</b></font> :: <code>any</code><br>
</li></ul><blockquote>The value in the map.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns <code>true</code> if the given value is stored somewhere in the map.<br>
</blockquote></li></ul></li></ul></li><li><u><b><i>is</i> Methods</b></u><br><br>
<ul><li><font color='#0052A3'>is( <font color='#006666'>…</font> )</font><b>,</b><font color='#0052A3'>isNot( <font color='#006666'>…</font> )</font><b>:: <code>boolean</code></b><br><br>
<ul><li><b>Accepted Types</b><br><br>
<ul><li><code>Map</code>
</li></ul><blockquote>Returns <code>true</code> if the given map has the same values stored under the same keys.<br>
</blockquote></li><li><b>Accepted <code>string</code> Values</b><br><br>
<ul><li><code>"empty"</code>
</li></ul><blockquote>Returns <code>true</code> if the current map is empty.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>is.<font color='#006666'>value</font></font><b>,</b><font color='#0052A3'>isNot.<font color='#006666'>value</font></font><b>:: <code>boolean</code></b><br><br>
<hr />
<h4><font color='#660000'>Timer</font></h4>
A simple timer for counting time intervals inside the script.<br>
</li></ul></li><li><u><b>Constructors</b></u><br><br>
<ul><li><font color='#0052A3'>Timer( <font color='#006666'>t</font> )</font><b>:: <code>Timer</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>t</b></font> :: <code>number</code><br>
</li></ul><blockquote>The countdown period in milliseconds.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns a new <code>Timer</code> object with the given countdown period. By default, the new timer is not "turned on". If you want the timer to start "ticking" right from the moment of creation use <code>reset</code> method like so: <code>Timer(3000).reset()</code>.<br>
</blockquote></li></ul></li></ul></li><li><u><b>Methods</b></u><br><br>
<ul><li><font color='#0052A3'>stop()</font><b>:: <code>self</code></b><br>
</li></ul><blockquote>Clears the map.<br>
</blockquote><ul><li><font color='#0052A3'>stopped()</font><b>:: <code>boolean</code></b><br>
</li></ul><blockquote>Returns <code>true</code> if the timer has stopped "ticking".<br>
</blockquote><ul><li><font color='#0052A3'>reset()</font><b>:: <code>self</code></b><br>
</li></ul><blockquote>Restarts the timer.<br>
</blockquote><ul><li><font color='#0052A3'>timeouted()</font><b>:: <code>boolean</code></b><br>
</li></ul><blockquote>Returns <code>true</code> if the timer has stopped "ticking" and restarts it. Otherwise, returns <code>false</code> and does nothing.<br>
<br>
<hr />
<h4><font color='#660000'>Logger</font></h4>
An advanced version of the <code>TraceAI</code> function(the one that produces output for command <b>/traceai</b>). Can output any object(even lists inside maps and so on) and data type to the specified file. A very useful tool for tracing the work of your script. This object also reacts to <b>/traceai</b> command(if the <code>LoggersUseTraceAI</code> <a href='http://code.google.com/p/raick/wiki/GettingStarted#Settings'>setting</a> is <code>ON</code>), but only on startup: if <b>/traceai</b> is turned off when the AI is being launched, then all loggers won't write anything. You would have to turn on <b>/traceai</b> and restart your AI to enable loggers again.<br>
<br>
All loggers create their files in the <code>Logs &amp; Errors</code> folder.<br>
</blockquote></li><li><u><b>Constructors</b></u><br><br>
<ul><li><font color='#0052A3'>Logger( <font color='#006666'>file</font> , <font color='#5E5B00'>delay</font> )</font><b>:: <code>Logger</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>file</b></font> :: <code>string</code><br>
</li></ul><blockquote>The name of the file.<br>
</blockquote><ul><li><font color='#5E5B00'><b>delay</b></font> | <code>0</code> :: <code>number</code><br>
</li></ul><blockquote>Logging delay(used in method <font color='#0052A3'><b>log()</b></font>).<br>
</blockquote></li><li><b>Description</b>
<blockquote>Creates a new <code>Logger</code>, which will write to the specified file with the specified delay.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>Logger( <font color='#006666'>file</font> , <font color='#5E5B00'>delimiter</font> )</font><b>:: <code>Logger</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>file</b></font> :: <code>string</code><br>
</li></ul><blockquote>The name of the file.<br>
</blockquote><ul><li><font color='#5E5B00'><b>delimiter</b></font> | <code>""</code> :: <code>string</code><br>
</li></ul><blockquote>The string that is used as a delimiter between the values being logged(used in methods <font color='#0052A3'><b>log()</b></font> and <font color='#0052A3'><b>write()</b></font>).<br>
</blockquote></li><li><b>Description</b>
<blockquote>Creates a new <code>Logger</code>, which will write to the specified file using the specified string as a delimiter between the values being outputted.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>Logger( <font color='#006666'>file</font> , <font color='#006666'>delay</font> , <font color='#006666'>delimiter</font> )</font><b>:: <code>Logger</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>file</b></font> :: <code>string</code><br>
</li></ul><blockquote>The name of the file.<br>
</blockquote><ul><li><font color='#006666'><b>delay</b></font> :: <code>number</code><br>
</li></ul><blockquote>Logging delay(used in method <font color='#0052A3'><b>log()</b></font>).<br>
</blockquote><ul><li><font color='#006666'><b>delimiter</b></font> :: <code>string</code><br>
</li></ul><blockquote>The string that is used as a delimiter between the values being logged(used in methods <font color='#0052A3'><b>log()</b></font> and <font color='#0052A3'><b>write()</b></font>).<br>
</blockquote></li><li><b>Description</b>
<blockquote>Creates a new <code>Logger</code>, which will write to the specified file with the specified delay, using the specified delimiter.<br>
</blockquote></li></ul></li></ul></li><li><u><b>Methods</b></u><br><br>
<ul><li><font color='#0052A3'>timeToLog()</font><b>:: <code>boolean</code>
</li></ul><blockquote>Returns <code>true</code> if the delay since the last log has ended.<br>
</blockquote><ul><li></b><font color='#0052A3'>resetTimer()</font><b>:: <code>self</code>
</li></ul><blockquote>Resets the delay timer.<br>
</blockquote><ul><li></b><font color='#0052A3'>log( <font color='#006666'><b>…</b></font> )</font><b>:: <code>self</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>…</b></font> :: <code>sequence</code><br>
</li></ul><blockquote>A sequence of values of any type.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Writes the current timestamp("date + time" string) to the <font color='#006666'><b>file</b></font> and(after that) textual representations of given values separating them with <font color='#006666'><b>delimiter</b></font>. For example:<br>
<pre><code><br>
logger = Logger("log.txt"," ")<br>
list = List(1,2,"abc")<br>
actor = Actor(100)<br>
<br>
logger.log("an actor:",actor,"and a list:",list)<br>
</code></pre>
Would output:<br><br>
<code>&gt; Week, DD Month, YYYY | HH:MM:SS &gt; an actor: Actor[ id=100 ] and a list: </code><br>
<code>List[ size=3 ]:</code>
<blockquote><code>( 1 )</code><br>
<code>( 2 )</code><br>
<code>( "abc" )</code><br>
</blockquote>Does nothing if <b>/traceai</b> is has been turned off during startup(only when <code>LoggersUseTraceAI</code> is <code>ON</code>) of AI or the delay since last log has not ended yet.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>write( <font color='#006666'><b>…</b></font> )</font><b>:: <code>self</code>
</li></ul><blockquote>The same as the previous method, except it does not put a timestamp and is not affected by the delay.<br>
</blockquote><ul><li></b><font color='#0052A3'>putTimestamp()</font><b>:: <code>self</code>
</li></ul><blockquote>Writes the timestamp("date + time" string) to the</b><font color='#006666'><b>file</b></font>.<br>
</blockquote><ul><li><font color='#0052A3'>newLine()</font><b>:: <code>self</code>
</li></ul><blockquote>"Presses the Enter key"(changes the line) in the</b><font color='#006666'><b>file</b></font>.<br>
</blockquote><ul><li><font color='#0052A3'>clear()</font><b>:: <code>self</code>
</li></ul><blockquote>Clear the</b><font color='#006666'><b>file</b></font>.<br>
</blockquote><ul><li><font color='#0052A3'>remove()</font><b>:: <code>self</code>
</li></ul><blockquote>Deletes the</b><font color='#006666'><b>file</b></font>.<br>
<br>
<hr />
<h4><font color='#660000'>Vector</font></h4>
Represents directions and positions of objects in relation to one another. Probably, the most hard-to-understand object, since it is directly related to math, but, actually, it is a very simple concept. Maps/locations in RO can be interpreted as 2D coordinate plains. No matter how you rotate your camera the plain remains the same: the direction of X-coordinate growth is the east and the Y-coordinate growth is the north. Suppose, you want to specify a direction of movement: what would you do? Well, one way of doing it is by "drawing an arrow" between 2 points. In math such arrows are called <i>vectors</i>. We can change the direction of the vector by changing the coordinates of its points. To simplify things we can fix the "tail" point to (0,0). Now we can easily define directions using only the "tip" point:<br>
<pre><code><br>
vector1 = Vector(1,0) -- Points to the east: an arrow from point (0,0) till (1,0)<br>
<br>
vector2 = Vector(3,-10) -- Points to the south-east<br>
</code></pre>
You're probably wondering how can vectors be used? Well, RAICK allows you to manipulate them with great ease! You can take a vector and a cell and calculate a new cell, which will be <code>n</code> cells away in the direction of the vector. For example, all actors including your owner have a motion vector. If you want your homunculus to stay behind the owner at a distance of 2 cells you can write something like this: <code>Homun.goTo(Owner.cell - Owner.vector * 2)</code>. This will tell your homunculus to go to a cell that is 2 cells away from where the owner is currently standing in the opposite direction of his current movement.<br>
Another way of defining vectors is by using 2 objects/cells. The idea is the same: you are drawing an "arrow" from one object to another, except what you get is a <i>relational</i> vector, which will define not the direction, but the position of one object in relation to another. A great example of this concept is putting traps right underneath the enemy feet:<br>
<pre><code><br>
vector = Vector(enemy, Merc) -- If the enemy is moving at us, then this vector will point in the direction of the movement<br>
<br>
if Merc .. enemy &lt;= 5 then -- If the enemy has gotten too close to the mercenary, then ..<br>
Merc.use(LandMine).on(enemy.cell + vector * 2) -- .. we put a mine between the bowman and the enemy.<br>
end<br>
</code></pre>
One final thing about vectors: 2 vectors with different coordinates can point in the same direction. How is that possible? It comes from the fact that you can define vectors with different <i>length</i>. For example: (1,1.5), (2,3), (4,6) would all point in the same direction, but if you draw them on a piece of paper you would see that they have different lengths. In math the length of the vector does indeed matter, but in RAICK it has no use meaning that for RAICK they are the same(when comparing them using the <code>==</code> operator or the <code>is</code> method).<br>
</blockquote></li><li><u><b>Constructors</b></u><br><br>
<ul><li><font color='#0052A3'>Vector( <font color='#5E5B00'>x</font> , <font color='#5E5B00'>y</font> )</font><b>:: <code>Vector</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#5E5B00'><b>x</b></font> :: <code>number</code> | <code>0</code><br>
</li></ul><blockquote>The X-coordinate of the vector.<br>
</blockquote><ul><li><font color='#5E5B00'><b>y</b></font> :: <code>number</code>| <code>0</code><br>
</li></ul><blockquote>The Y-coordinate of the vector.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Return a new <code>Vector</code> pointing in direction specified by (<font color='#5E5B00'><b>x</b></font>,<font color='#5E5B00'><b>y</b></font>) coordinates. If both coordinates are not specified, then returns a <i>null vector</i>, which indicates an absence of a direction(for example, "standing" is case of a motion vector).<br>
</blockquote></li></ul></li><li><font color='#0052A3'>Vector( <font color='#006666'>object1</font> , <font color='#006666'>object2</font> )</font><b>:: <code>Vector</code> | <code>nil</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>object1</b></font> :: <code>Cell</code> | <code>Actor</code> | <code>Owner</code> |  <code>Homunculus</code> |  <code>Mercenary</code><br>
</li></ul><blockquote>The object, in relation to which the vector is calculated.<br>
</blockquote><ul><li><font color='#006666'><b>object2</b></font> :: <code>Cell</code> | <code>Actor</code> | <code>Owner</code> |  <code>Homunculus</code> |  <code>Mercenary</code><br>
</li></ul><blockquote>The object, which defines the direction of the vector in relation to <font color='#006666'><b>object1</b></font>.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Return a new <code>Vector</code> pointing in the direction specified by <font color='#006666'><b>object2</b></font> in relation to <font color='#006666'><b>object1</b></font>(an "arrow" drawn from <font color='#006666'><b>object1</b></font> till <font color='#006666'><b>object2</b></font>) or <code>nil</code> if at least one of the objects in not visible.<br>
</blockquote></li></ul></li></ul></li><li><u><b>Fields</b></u><br><br>
<ul><li><font color='#006666'><b>x</b></font> :: <code>number</code><br>
</li></ul><blockquote>The X-coordinate of the vector.<br>
</blockquote><ul><li><font color='#006666'><b>y</b></font> :: <code>number</code><br>
</li></ul><blockquote>The Y-coordinate of the vector.<br>
</blockquote></li><li><u><b><i>is</i> Methods</b></u><br><br>
<ul><li><font color='#0052A3'>is( <font color='#006666'>…</font> )</font><b>,</b><font color='#0052A3'>isNot( <font color='#006666'>…</font> )</font><b>:: <code>boolean</code></b><br><br>
<ul><li><b>Accepted Types</b><br><br>
<ul><li><code>Vector</code>
</li></ul><blockquote>Returns <code>true</code> if the given vector is pointing in the same direction as the current one.<br>
</blockquote></li><li><b>Accepted <code>string</code> Values</b><br><br>
<ul><li><code>"none"</code>
</li></ul><blockquote>Returns <code>true</code> if the current vector has (0,0) coordinates.<br>
</blockquote><ul><li><code>"north"</code>
</li></ul><blockquote>Returns <code>true</code> if the current vector is pointing to north of the current location/map.<br>
</blockquote><ul><li><code>"south"</code>
</li></ul><blockquote>Returns <code>true</code> if the current vector is pointing to south of the current location/map.<br>
</blockquote><ul><li><code>"west"</code>
</li></ul><blockquote>Returns <code>true</code> if the current vector is pointing to west of the current location/map.<br>
</blockquote><ul><li><code>"east"</code>
</li></ul><blockquote>Returns <code>true</code> if the current vector is pointing to east of the current location/map.<br>
</blockquote><ul><li><code>"northWest"</code>
</li></ul><blockquote>Returns <code>true</code> if the current vector is pointing to north-west of the current location/map.<br>
</blockquote><ul><li><code>"southWest"</code>
</li></ul><blockquote>Returns <code>true</code> if the current vector is pointing to south-west of the current location/map.<br>
</blockquote><ul><li><code>"northEast"</code>
</li></ul><blockquote>Returns <code>true</code> if the current vector is pointing to north-east of the current location/map.<br>
</blockquote><ul><li><code>"southEast"</code>
</li></ul><blockquote>Returns <code>true</code> if the current vector is pointing to south-east of the current location/map.<br>
</blockquote><ul><li><code>"[x];[y]"</code>
</li></ul><blockquote>Returns <code>true</code> if the current vector is pointing in the same direction as the vector with (<code>[x]</code>,<code>[y]</code>) coordinates. The delimiter ; can be replaced with anything you want as long as it is not a number, dot or minus.  For example <code>"-1;2"</code>, <code>"0.252|1"</code>.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>is.<font color='#006666'>value</font></font><b>,</b><font color='#0052A3'>isNot.<font color='#006666'>value</font></font><b>:: <code>boolean</code></b><br><br>
</li></ul></li><li><u><b>Operators</b></u><br><br>
<ul><li><font color='#0052A3'><font color='#006666'>cell</font> + <font color='#006666'>vector</font> <code>*</code> <font color='#5E5B00'>distance</font></font><b>:: <code>Cell</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>cell</b></font> :: <code>Cell</code><br>
</li></ul><blockquote>An arbitrary <code>Cell</code> object.<br>
</blockquote><ul><li><font color='#006666'><b>vector</b></font> :: <code>Vector</code><br>
</li></ul><blockquote>An arbitrary <code>Vector</code> object.<br>
</blockquote><ul><li><font color='#5E5B00'><b>distance</b></font> | <code>1</code> :: <code>number</code><br>
</li></ul><blockquote>The distance, by which the <font color='#006666'>cell</font><b>will be shifted in the direction of</b><font color='#006666'>vector</font><b>. Negative values will shift it in the opposite direction.</b><br>
</blockquote></li><li><b>Description</b>
<blockquote>This equation returns the cell, which is <font color='#5E5B00'>distance</font><b>cells away from the</b><font color='#006666'>cell</font><b>in the direction defined by</b><font color='#006666'>vector</font><b>.<br>
</blockquote></li></ul></li><li></b><font color='#0052A3'>- <font color='#006666'>vector</font></font><b>:: <code>Vector</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>vector</b></font> :: <code>Cell</code><br>
</li></ul><blockquote>An arbitrary <code>Vector</code> object.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns a new <code>Vector</code> pointing to the opposite direction of <font color='#006666'><b>vector</b></font>.<br>
<br>
<hr />
<h3><font color='#006600'>Single Objects</font></h3>
<code>Owner</code>, <code>Homunculus</code> and <code>Mercenary</code> objects have multiple global variables defined for them to free you from the labor of writing long names like <code>Mercenary</code> or <code>Homunculus</code>. Shorter versions start from the third letter of the type name. For example, <code>Owner</code> object has 3 variables:<br>
</blockquote></li></ul></li></ul><ul><li>Own<br>
</li><li>Owne<br>
</li><li>Owner<br>
<h4><font color='#660000'>Owner</font></h4>
Represents your character.<br>
Most of the fields repeat the ones that the <a href='http://code.google.com/p/raick/wiki/Manual#Actor'>Actor</a> object has, since your character is also an actor, so I won't bother describing them. The HP and SP field description is also unnecessary, since everything has been already explained in the <a href='http://code.google.com/p/raick/wiki/Manual#Points'>appropriate section</a>.<br>
</li></ul></li><li><u><b>Fields</b></u><br><br>
<ul><li><font color='#006666'><b>id</b></font> :: <code>number</code><br><br>
</li><li><font color='#006666'><b>cell</b></font> :: <code>Cell</code><br><br>
</li><li><font color='#006666'><b>prev.cell</b></font> :: <code>Cell</code><br><br>
</li><li><font color='#006666'><b>last.cell</b></font> :: <code>Cell</code><br><br>
</li><li><font color='#006666'><b>action</b></font> :: <code>Value</code><br><br>
</li><li><font color='#006666'><b>prev.action</b></font> :: <code>Value</code><br><br>
</li><li><font color='#006666'><b>last.action</b></font> :: <code>Value</code><br><br>
</li><li><font color='#006666'><b>target</b></font> :: <code>Actor</code> | <code>Owner</code> |  <code>Homunculus</code> |  <code>Mercenary</code><br><br>
</li><li><font color='#006666'><b>prev.target</b></font> :: <code>Actor</code> | <code>Owner</code> |  <code>Homunculus</code> |  <code>Mercenary</code><br><br>
</li><li><font color='#006666'><b>last.target</b></font> :: <code>Actor</code> | <code>Owner</code> |  <code>Homunculus</code> |  <code>Mercenary</code><br><br>
</li><li><font color='#006666'><b>type</b></font> :: <code>Value</code><br><br>
</li><li><font color='#006666'><b>vector</b></font> :: <code>Vector</code><br><br>
</li><li><font color='#006666'><b>prev.vector</b></font> :: <code>Vector</code><br><br>
</li><li><font color='#006666'><b>last.vector</b></font> :: <code>Vector</code><br><br>
</li><li><font color='#006666'><b>hp</b></font> :: <code>Points</code><br><br>
</li><li><font color='#006666'><b>prev.hp</b></font> :: <code>Points</code><br><br>
</li><li><font color='#006666'><b>last.hp</b></font> :: <code>Points</code><br><br>
</li><li><font color='#006666'><b>sp</b></font> :: <code>Points</code><br><br>
</li><li><font color='#006666'><b>prev.sp</b></font> :: <code>Points</code><br><br>
</li><li><font color='#006666'><b>last.sp</b></font> :: <code>Points</code><br><br>
</li><li><font color='#006666'><b>visionRange</b></font> :: <code>number</code>
</li></ul><blockquote>The vision range that is defined using the <code>VisionRange</code> <a href='http://code.google.com/p/raick/wiki/GettingStarted#Settings'>setting</a>.<br>
</blockquote><ul><li><font color='#006666'><b>surround</b></font> :: <code>List</code>
</li></ul><blockquote>All actors that are currently visible on the screen(in range of vision).<br>
</blockquote><ul><li><font color='#006666'><b>prev.surround</b></font> :: <code>List</code>
</li></ul><blockquote>All actors that were visible on the screen(in range of vision) in the previous moment of time.<br>
</blockquote><ul><li><font color='#006666'><b>fullSurround</b></font> :: <code>List</code>
</li></ul><blockquote>All actors that are currently on the screen(in range of vision).<br>
</blockquote><ul><li><font color='#006666'><b>prev.fullSurround</b></font> :: <code>List</code>
</li></ul><blockquote>All actors that were on on the screen(in range of vision) in the previous moment of time.<br>
</blockquote></li><li><u><b><i>is</i> Methods</b></u><br><br>
<ul><li><font color='#0052A3'>is( <font color='#006666'>…</font> )</font><b>,</b><font color='#0052A3'>isNot( <font color='#006666'>…</font> )</font><b>:: <code>boolean</code></b><br><br>
<ul><li><b>Accepted <code>string</code> Values</b><br><br>
<ul><li><code>"full"</code>
</li></ul><blockquote>Returns <code>true</code> if your character's HP and SP are full.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>is.<font color='#006666'>value</font></font><b>,</b><font color='#0052A3'>isNot.<font color='#006666'>value</font></font><b>:: <code>boolean</code></b><br><br>
</li></ul></li><li><u><b>Operators</b></u><br><br>
<ul><li><font color='#0052A3'><font color='#006666'>owner</font> .. <font color='#006666'>object</font></font><b>:: <code>number</code> | <code>nil</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>owner</b></font> :: <code>Owner</code><br>
</li></ul><blockquote>The <code>Owner</code> object.<br>
</blockquote><ul><li><font color='#006666'><b>object</b></font> :: <code>Cell</code> | <code>Actor</code> | <code>Owner</code> |  <code>Homunculus</code> |  <code>Mercenary</code><br>
</li></ul><blockquote>Any in-game object, distance till which you want to know.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns the distance(in cells) between you and <font color='#006666'><b>object</b></font> or <code>nil</code> if <font color='#006666'><b>object</b></font> is an actor, which is not visible.<br>
<br>
<hr />
<h4><font color='#660000'>Homunculus / Mercenary</font></h4>
I will unify descriptions of these objects, since they are identical.<br>
They represent your homunculus/mercenary and are both defined in the homunculus and in the mercenary AI's, since RAICK support data exchange between scripts. Read more about it in the <a href='http://code.google.com/p/raick/wiki/Manual#Data_Exchange_Between_Homunculus_and_Mercenary'>last section</a>.<br>
Most of the fields repeat the ones that the <a href='http://code.google.com/p/raick/wiki/Manual#Actor'>Actor</a> object has, since your homunculus/mercenary is also an actor, so I won't bother describing them. The HP and SP field description is also unnecessary, since everything has been already explained in the <a href='http://code.google.com/p/raick/wiki/Manual#Points'>appropriate section</a>.<br>
</blockquote></li></ul></li></ul></li><li><u><b>Fields</b></u><br><br>
<ul><li><font color='#006666'><b>id</b></font> :: <code>number</code><br><br>
</li><li><font color='#006666'><b>cell</b></font> :: <code>Cell</code><br><br>
</li><li><font color='#006666'><b>prev.cell</b></font> :: <code>Cell</code><br><br>
</li><li><font color='#006666'><b>last.cell</b></font> :: <code>Cell</code><br><br>
</li><li><font color='#006666'><b>action</b></font> :: <code>Value</code><br><br>
</li><li><font color='#006666'><b>prev.action</b></font> :: <code>Value</code><br><br>
</li><li><font color='#006666'><b>last.action</b></font> :: <code>Value</code><br><br>
</li><li><font color='#006666'><b>target</b></font> :: <code>Actor</code> | <code>Owner</code> |  <code>Homunculus</code> |  <code>Mercenary</code><br><br>
</li><li><font color='#006666'><b>prev.target</b></font> :: <code>Actor</code> | <code>Owner</code> |  <code>Homunculus</code> |  <code>Mercenary</code><br><br>
</li><li><font color='#006666'><b>last.target</b></font> :: <code>Actor</code> | <code>Owner</code> |  <code>Homunculus</code> |  <code>Mercenary</code><br><br>
</li><li><font color='#006666'><b>type</b></font> :: <code>Value</code><br><br>
</li><li><font color='#006666'><b>vector</b></font> :: <code>Vector</code><br><br>
</li><li><font color='#006666'><b>prev.vector</b></font> :: <code>Vector</code><br><br>
</li><li><font color='#006666'><b>last.vector</b></font> :: <code>Vector</code><br><br>
</li><li><font color='#006666'><b>hp</b></font> :: <code>Points</code><br><br>
</li><li><font color='#006666'><b>prev.hp</b></font> :: <code>Points</code><br><br>
</li><li><font color='#006666'><b>last.hp</b></font> :: <code>Points</code><br><br>
</li><li><font color='#006666'><b>sp</b></font> :: <code>Points</code><br><br>
</li><li><font color='#006666'><b>prev.sp</b></font> :: <code>Points</code><br><br>
</li><li><font color='#006666'><b>last.sp</b></font> :: <code>Points</code><br><br>
</li><li><font color='#006666'><b>hit.range</b></font> :: <code>number</code>
</li></ul><blockquote>The range of a normal attack in cells.<br>
</blockquote></li><li><u><b>Methods</b></u><br><br>
<ul><li><font color='#0052A3'>goTo( <font color='#006666'>v</font> , <font color='#5E5B00'>n</font> )</font><b>:: <code>self</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>v</b></font> :: <code>Cell</code> | <code>Actor</code> | <code>Owner</code> | <code>Mercenary</code>/<code>Homunculus</code> | <code>Vector</code><br>
</li></ul><blockquote>The location or the in-game character, to which the homunculus/mercenary must go or the direction(vector) of it's movement.<br>
</blockquote><ul><li><font color='#5E5B00'><b>n</b></font> :: <code>number</code><br>
</li></ul><blockquote>The number of cells, by which the homunculus/mercenary must advance in the direction specified by the location, object or vector.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Orders your homunculus/mercenary to go to the specified cell or to the cell, on which the specified object stand on or in the direction specified by the vector. The second argument is used to modify the length of path that the homunculus/mercenary is allowed to go through. If <font color='#006666'><b>v</b></font> is a <code>Vector</code>, then <font color='#5E5B00'><b>n</b></font> specifies the number of cells that the homunculus/mercenary should go through in the direction of the vector. In other cases:<br><br>
<ul><li><font color='#5E5B00'><b>n</b></font> is a fractional value between 0 and 1<br>
</li></ul><blockquote>The homunculus/mercenary will go through (<font color='#5E5B00'><b>n</b></font> <code>*</code> 100)% of the path.<br>
</blockquote><ul><li><font color='#5E5B00'><b>n</b></font> is a fractional value between -1 and 0<br>
</li></ul><blockquote>The homunculus/mercenary will go through ((1 + <font color='#5E5B00'><b>n</b></font>) <code>*</code> 100)% of the path.<br>
</blockquote><ul><li><font color='#5E5B00'><b>n</b></font> >= 1<br>
</li></ul><blockquote>The homunculus/mercenary will go through <font color='#5E5B00'><b>n</b></font> cells along the path.<br>
</blockquote><ul><li><font color='#5E5B00'><b>n</b></font> <= -1<br>
</li></ul><blockquote>The homunculus/mercenary will keep <font color='#5E5B00'><b>n</b></font> cells away from <font color='#006666'><b>v</b></font>.<br>
</blockquote></blockquote></li></ul></li><li><font color='#0052A3'>hit( <font color='#006666'>target</font> )</font><b>:: <code>self</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>target</b></font> :: <code>Actor</code><br>
</li></ul><blockquote>The target.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Orders your homunculus/mercenary to hit(attack with normal attacks) the specified target once.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>use( <font color='#006666'>skill</font> , <font color='#5E5B00'>lvl</font> )</font><b>:: <code>self</code>
</li><li></b><font color='#0052A3'>use( <font color='#006666'>skill</font> , <font color='#5E5B00'>lvl</font> ).on( <font color='#006666'>target</font> )</font><b>:: <code>self</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>skill</b></font> :: <code>Skill</code><br>
</li></ul><blockquote>The skill that you want your homunculus/mercenary to use.<br>
</blockquote><ul><li><font color='#5E5B00'><b>lvl</b></font> :: <code>number</code> | <font color='#006666'><b>skill.maxLevel</b></font><br>
</li></ul><blockquote>The level of the skill.<br>
</blockquote><ul><li><font color='#006666'><b>target</b></font> :: <code>Actor</code><br>
</li></ul><blockquote>The target, on which the skill should be used.<br>
</blockquote></li><li><b>Description</b>
<blockquote>The first version of this method is used for non-targeted skills and the second one is for targeted ones. If the level of the skill is omitted uses the maximum level available.<br>
</blockquote></li></ul></li></ul></li><li><u><b><i>is</i> Methods</b></u><br><br>
<ul><li><font color='#0052A3'>is( <font color='#006666'>…</font> )</font><b>,</b><font color='#0052A3'>isNot( <font color='#006666'>…</font> )</font><b>:: <code>boolean</code></b><br><br>
<ul><li><b>Accepted <code>string</code> Values</b><br><br>
<ul><li><code>"full"</code>
</li></ul><blockquote>Returns <code>true</code> if homunculus'/mercenaries HP and SP are full.<br>
</blockquote><ul><li><code>"active"</code>
</li></ul><blockquote>Returns <code>true</code> if the object is active. Explained in the <a href='http://code.google.com/p/raick/wiki/Manual#Data_Exchange_Between_Homunculus_and_Mercenary'>last section</a>.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>is.<font color='#006666'>value</font></font><b>,</b><font color='#0052A3'>isNot.<font color='#006666'>value</font></font><b>:: <code>boolean</code></b><br><br>
</li></ul></li><li><u><b>Operators</b></u><br><br>
<ul><li><font color='#0052A3'><font color='#006666'>homun/merc</font> .. <font color='#006666'>object</font></font><b>:: <code>number</code> | <code>nil</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>homun/merc</b></font> :: <code>Homunculus</code>/<code>Mercenary</code><br>
</li></ul><blockquote>The <code>Homunculus</code>/<code>Mercenary</code> object.<br>
</blockquote><ul><li><font color='#006666'><b>object</b></font> :: <code>Cell</code> | <code>Actor</code> | <code>Owner</code> |  <code>Homunculus</code> |  <code>Mercenary</code><br>
</li></ul><blockquote>Any in-game object, distance till which you want to know.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns the distance(in cells) between your homunculus/mercenary and <font color='#006666'><b>object</b></font> or <code>nil</code> if <font color='#006666'><b>object</b></font> is an actor, which is not visible.<br>
<br>
<hr />
<h4><font color='#660000'>Memory</font></h4>
The object for manipulating the memory. Values are saved under <code>string</code> keys just like in an ordinary table. I will refer to those strings as <i>memory variables</i> or <i>entries</i>. As an exception to the common rule: memory variables are case and delimiter <u>sensitive</u>. Read more about the memory file <a href='http://code.google.com/p/raick/wiki/Manual#0._Memory'>here</a>.<br>
</blockquote></li></ul></li></ul></li><li><u><b>Methods</b></u><br><br>
<ul><li><font color='#0052A3'>save( <font color='#006666'>n</font> , <font color='#006666'>v</font> )</font><b>::</b><font color='#006666'><b>v</b></font><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>n</b></font> :: <code>string</code><br>
</li></ul><blockquote>The name of the memory variable.<br>
</blockquote><ul><li><font color='#006666'><b>v</b></font> :: <code>number</code> | <code>string</code> | <code>boolean</code> | <code>Value</code> | <code>Cell</code> | <code>Actor</code> | <code>Vector</code><br><code>List</code> ( <code>number</code> | <code>string</code> | <code>boolean</code> | <code>Value</code> | <code>Cell</code> | <code>Actor</code> | <code>Vector</code> )<br><code>Map</code> ( <code>number</code> | <code>string</code> | <code>boolean</code> | <code>Value</code> | <code>Cell</code> | <code>Actor</code> | <code>Vector</code> )<br>
</li></ul><blockquote>The value that needs to be saved. The type restriction above says that only the mentioned types can be saved to the memory and if you want to save a <code>List</code> or a <code>Map</code>, then they also must contains only those types.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Saves <font color='#006666'><b>v</b></font> to memory variable <font color='#006666'><b>n</b></font> and return <font color='#006666'><b>v</b></font> afterwards.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>get( <font color='#006666'>n</font> , <font color='#5E5B00'>v</font> )</font><b>:: <code>any</code> |</b><font color='#5E5B00'><b>v</b></font> | <code>nil</code><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>n</b></font> :: <code>string</code><br>
</li></ul><blockquote>The name of the memory variable.<br>
</blockquote><ul><li><font color='#5E5B00'><b>v</b></font> :: <code>any</code><br>
</li></ul><blockquote>The value that will be returned if <font color='#006666'><b>n</b></font> does not exist in the memory.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns the value that is saved to <font color='#006666'><b>n</b></font> or <font color='#5E5B00'><b>v</b></font> if no such entry exist or <code>nil</code> if no such entry exist and <font color='#5E5B00'><b>v</b></font> is omitted.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>contains( <font color='#006666'>n</font> )</font><b>:: <code>boolean</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>n</b></font> :: <code>string</code><br>
</li></ul><blockquote>The name of the memory variable.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Returns <code>true</code> if the entry <font color='#006666'><b>n</b></font> exist in the memory.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>delete( <font color='#006666'>n</font> )</font><b>:: <code>self</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>n</b></font> :: <code>string</code><br>
</li></ul><blockquote>The name of the memory variable.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Deletes entry <font color='#006666'><b>n</b></font> from the memory.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>clear()</font><b>:: <code>self</code>
</li></ul><blockquote>Clears the memory including RAICK service data like current activity or activity arguments(the values in script variables will still be available until the restart).<br></b><br>
<hr />
<h4><font color='#660000'>Activity</font></h4>
Through this object you can change the current activity of your homunculus/mercenary or get information about the current or the last activity. Read more about activities <a href='http://code.google.com/p/raick/wiki/Manual#5._Activities'>here</a>.<br>
</blockquote></li><li><u><b>Fields</b></u><br><br>
<ul><li><font color='#006666'><b>current</b></font> :: <code>Value</code><br><br>
</li></ul><blockquote>Contains the name of the current activity and it's sequential number(the first activity would get 1 and so on). This value "survives" the restart of the script, since it is automatically saved to memory.<br>
</blockquote><ul><li><font color='#006666'><b>last</b></font> :: <code>Value</code> | <code>nil</code><br><br>
</li></ul><blockquote>Contains the name of the last activity(the one that your homunculus/mercenary was before the switching to the current activity) and it's sequential number or <code>nil</code> if the AI is run for the first time and there is historical data available.<br>
</blockquote></li><li><u><b>Methods</b></u><br><br>
<ul><li><font color='#0052A3'>switchTo.<font color='#006666'>activity</font>( <font color='#5E5B00'>…</font> )</font><b>:: <code>self</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>activity</b></font> :: <code>string</code><br>
</li></ul><blockquote>The name of the activity.<br>
</blockquote><ul><li><font color='#5E5B00'><b>…</b></font> :: <code>sequence</code> ( <code>number</code> | <code>string</code> | <code>boolean</code> | <code>Value</code> | <code>Cell</code> | <code>Actor</code> |  <code>Points</code> |  <code>Skill</code> | <code>Vector</code> )<br>
</li></ul><blockquote>A sequence of values with arbitrary number of elements.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Switches your homunculus/mercenary to <font color='#006666'><b>activity</b></font> activity with given arguments. Two <font color='#006666'><b>activity</b></font> names have special meaning:<br><br>
<ul><li><code>initial</code>
</li></ul><blockquote>Switches to the first state that is defined in the <code>Activities</code> file.<br>
</blockquote><ul><li><code>last</code>
</li></ul><blockquote>Switches to the <font color='#006666'><b>last</b></font> activity or does nothing if it is <code>nil</code>.<br>
</blockquote>As always, <font color='#006666'><b>activity</b></font> is case and delimiter insensitive.<br>
</blockquote></li></ul></li><li><font color='#0052A3'>changeArgument( <font color='#006666'>n</font> , <font color='#006666'>v</font> )</font><b>:: <code>self</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>n</b></font> :: <code>string</code><br>
</li></ul><blockquote>The sequential number of the argument(starting from 1).<br>
</blockquote><ul><li><font color='#006666'><b>v</b></font> :: <code>number</code> | <code>string</code> | <code>boolean</code> | <code>Value</code> | <code>Cell</code> | <code>Actor</code> |  <code>Points</code> |  <code>Skill</code> | <code>Vector</code><br>
</li></ul><blockquote>The new value of the argument.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Changes the <font color='#006666'><b>n</b></font>'th argument of the current activity to <font color='#006666'><b>v</b></font>.<br>
<br>
<hr />
<h2><font color='#006666'>Detailed Overview of Files</font></h2>
Partially this topic is covered in the <a href='http://code.google.com/p/raick/wiki/GettingStarted#AI_Specific_Files'>Getting Started</a> chapter. I will just introduce the facts that'll complete the picture.<br>
All of RAICK's AI files share one common feature, which simplifies and quickens the scripting process. The idea is quite simple: global variables with <i>special</i> names are translated into strings. What this means is that, for example, if you are querying a global variable <code>visible</code>(and this variable contains <code>nil</code>- it has not been used or has been cleared after usage), then the result of the query will be string <code>"visible"</code>. So, how do you know which names are <i>special</i>? Here is the list:<br>
</blockquote></li></ul></li></ul></li><li>Status names(<font color='#006666'><b>status</b></font> field)<br>
</li><li>Group names(<font color='#006666'><b>group</b></font> field)<br>
</li><li>Type names(<font color='#006666'><b>type</b></font> field) ›› <i>! Every monster !</i>
Like (pretty much) everywhere in RAICK the names are case and delimiter insensitive meaning that, for example, <code>ma__Ya__Pu__rple</code> is also translated into a string just like <code>MayaPurple</code>. This also concerns the names of handler functions and activities discussed below. For example: <code>a_l_t_shift_TARGET</code> and <code>AltShiftTarget</code> refer to the same handler function.<br>
<h3><font color='#006600'>0. Memory</font></h3>
The memory file is automatically created and managed by RAICK. This is where your saved values are stored. If you open it, you will first of all see a header saying when the memory was last updated and how many percent of it's capacity is currently taken. The header is followed by the list of entries, each of them with it's own small header, which specifies the type of the value, as well as the number of elements if the value is a <code>List</code> or a <code>Map</code>. Values between underscores like <code>_s_</code> are RAICK service memory entries- they should not be altered.<br>
<br>
The file itself can be manually altered, but if you make any mistakes you won't be able to run your AI properly until you either fix the error or delete the memory file.<br>
<br>
<hr />
<h3><font color='#006600'>1. On Startup</font></h3>
The content of this file is run only once, when your AI is being loaded. This is the only file that is not pre-processed meaning that everything you define here will be visible in all parts of your script exactly the way it is defined. Typically, you will use this file to put initial values to your variables or to define your own custom functions.<br>
If you want to add your own script files to this file using <code>require</code>(for example, some functions from your self-made library), then RAICK offers a convenient way of doing so. You just have to name your file <code>"[1] XXX.lua"</code>(where XXX if the name you want) and then add a call to the <code>require</code> function somewhere in the <code>On Startup</code> file like so:<br>
<pre><code><br>
require "XXX" -- You don't have to write neither the prefix nor the extension of the file!<br>
</code></pre>
This way you will not break the ordering of files and make your own little library a logical part of the whole framework.<br>
<br><br>
<hr />
<h3><font color='#006600'>2. Commands</font></h3>
The file, where you define <i>handler</i> functions that intercept <code>Ctrl + Something</code> or <code>Alt + Something</code> commands. Upon creation it is automatically filled with all available command handlers. The usage is straightforward: the name refers to the key combination and the arguments are either the cell or the target actor that you click on.<br>
Anything other than the handler functions will be ignored.<br>
<br>
<hr />
<h3><font color='#006600'>3. XXX Skills</font></h3>
Files, where you define <i>handler</i> functions that intercept commands to use a targeted skill. Upon creation it is also automatically filled with all available skill handlers. The second argument is always the skill level used and the first one is either a cell or an actor depending of the type of the skill: ground- or enemy-targeted.<br>
Anything other than the handler functions will be ignored.<br>
<br>
<hr />
<h3><font color='#006600'>4. Messages</font></h3>
The file, where you define <i>handler</i> functions that intercept messages sent from one AI script to another. This allows your bots to communicate with each other. You can read more about this wonderful feature in the <a href='http://code.google.com/p/raick/wiki/Manual#Data_Exchange_Between_Homunculus_and_Mercenary'>last section</a>.<br>
<br>
<hr />
<h3><font color='#006600'>5. Activities</font></h3>
The final and the most important file is the one, where you define your activities. The first activity that you define is called <i>initial</i>. When you run your script for the first time RAICK does not know what is the current activity(since the memory is empty), so it uses the first activity as the current one.<br>
Two activity names are <i>special</i>: <code>pre</code> and <code>post</code>(plus all case and delimiter insensitive variations). The first one is called every time before the current activity function is called and the second one is called after the current activity executes. Typically, you would use those to define periodical events like casting self-support skills.<br>
There is also one hidden activity, to which your bot is switched if RAICK encounters an error in your script. In this activity your bot will follow you and you will have an ability to manually use it's skills. You can think of it as a <i>Safe Mode</i>.<br>
Activities can take arguments, which are automatically saved to the memory.<br>
<br>
<hr />
<h2><font color='#006666'>Understanding RAICK Errors</font></h2>
Whenever RAICK encounters an error inside your script or inside the framework itself it generates a descriptive report about the type and the cause of the error. This report is then showed to the user in the error window and documented to the <code>Logs &amp; Errors/Error Logs.txt</code> file or to the <code>RAICK.Bugz.txt</code> file in case the error came from RAICK. Finally, your bot is switched to the <i>Safe Mode</i> to cut-off the possibility of the error occurring again.<br>
The error report may contain following rows:<br>
</li><li><code>[!] ERROR TYPE [!]</code>
</li></ul><blockquote>The type of the error. Can be:<br>
<ul><li><code>ERROR IN SETTINGS</code>
</li></ul><blockquote>You have made an error in <code>RAICK.Settings.lua</code> file.<br>
</blockquote><ul><li><code>SYNTAX ERROR</code>
</li></ul><blockquote>You have made a syntactical error somewhere in your script.<br>
</blockquote><ul><li><code>INVALID ARGUMENT ERROR</code>
</li></ul><blockquote>An invalid argument has been given to a function.<br>
</blockquote><ul><li><code>MEMORY OVERFLOW ERROR</code>
</li></ul><blockquote>You have exceeded the capacity of the memory.<br>
</blockquote><ul><li><code>LUA ERROR</code>
</li></ul><blockquote>A typical Lua error that RAICK is unable to classify.<br>
</blockquote></blockquote><ul><li><code>File</code>
</li></ul><blockquote>The file, where the error has occurred.<br>
</blockquote><ul><li><code>Line</code>
</li></ul><blockquote>The line of the file, on which the error occurred.<br>
</blockquote><ul><li><code>Cause</code>
</li></ul><blockquote>Why the error occurred.<br>
</blockquote><ul><li><code>Function</code>/<code>Operator</code>
</li></ul><blockquote>The name of the function, method or operator, which was used incorrectly.<br>
</blockquote><ul><li><code>Argument</code>
</li></ul><blockquote>The sequential number(or place relative to the operator: left, right) of the invalid argument.<br>
</blockquote><ul><li><code>Expected</code>
</li></ul><blockquote>The correct type or value of the argument.<br>
</blockquote><ul><li><code>Got</code>
</li></ul><blockquote>The received/incorrect type or value of the argument.<br>
</blockquote><ul><li><code>Solution</code>
</li></ul><blockquote>What RAICK will do or has done to fix the problem.<br>
</blockquote><ul><li><code>[!] ATTENTION [!]</code> footer<br>
</li></ul><blockquote>If you see a footer starting with this row, then the error is the bug of the framework, not your script. You should report about it as soon as possible.<br>
<br>
<hr />
<h2><font color='#006666'>Data Exchange Between Homunculus and Mercenary</font></h2>
A truly unique feature of RAICK is the ability to unify two scripts in one making bot communication painless and a joy to use.<br>
So, here's how it works. First of all, you have to turn <code>ON</code> the <code>BotCommunication</code> setting and restart both of your scripts(<i>Character Select</i> is the best way to do it, since mercenaries cannot be <i>Rest</i>'ed). The <code>Homunculus</code> object in the mercenary AI and the <code>Mercenary</code> object in the homunculus AI will now "come to life". They will fully replicate the "original" objects(all fields + all methods) from the corresponding/opposite AI's as long as the second bot(i call it <i>cobot</i>) is in range of vision. The fact that the cobot is in your sight can be checked through the <code>is</code> method: <code>is.active</code> returns <code>true</code> if the cobot is in range of sight. When the object is inactive the methods will not function and it won't contain any data.<br>
Just think about it! Basically, you can use only one AI to control both of your bots! And there is even something extra! Besides having total control over the actions and the data of the cobot you can also send messages to it using the following method, which appears inside the bot object(the original object inside it's AI) if the communication is turned <code>ON</code>:<br>
</blockquote><ul><li><font color='#0052A3'>send.<font color='#006666'>message</font>( <font color='#006666'>value</font> )</font><b>:: <code>self</code></b><br><br>
<ul><li><b>Arguments</b><br><br>
<ul><li><font color='#006666'><b>message</b></font> :: <code>string</code><br>
</li></ul><blockquote>The name of the message.<br>
</blockquote><ul><li><font color='#006666'><b>value</b></font> :: <code>number</code> | <code>string</code> | <code>boolean</code> | <code>Value</code> | <code>Cell</code> | <code>Actor</code> |  <code>Points</code> |  <code>Skill</code> | <code>Vector</code><br>
</li></ul><blockquote>The value that you want to send.<br>
</blockquote></li><li><b>Description</b>
<blockquote>Calls the <font color='#006666'><b>message</b></font> handler function defined in the <code>Messages</code> file of the cobot's AI passing the <font color='#006666'><b>value</b></font> to it. If the handler function with this name(plus all case and delimiter insensitive variations) is not defined, then nothing happens. During a single execution of the activity(call of the AI by the client) only one value can be sent using this method.<br>
Using this method you can send values of specified data types to the opposite side. The second AI will receive them through handler functions defined in the <code>Messages</code> file. Every such function must be defined with one argument to be able to receive those values. For example:<br>
<pre><code><br>
-- Somewhere in the Homunculus AI:<br>
Homun.send.killHim(actor)<br>
...<br>
-- In the Messages file of the Mercenary AI:<br>
function    KILL_HIM(enemy)<br>
<br>
mainTarget = Memory.save("mainTarget", enemy)<br>
Activity.switchTo.terminationOf(mainTarget)<br>
end<br>
</code></pre>
<br>
<hr />
<h2><font color='#006666'>Quick Reload</font></h2>
Another unique feature of RAICK that allows you to update your AI literally on-the-fly. When the setting <code>QuickReload</code> is turned <code>ON</code>, changes to <code>Commands</code>, <code>Skills</code> or <code>Activities</code> files automatically trigger the reload of this file i.e. all handler functions are recreated as if you have restarted your AI. This liberates you from restarting your AI every time you want to change something.<br>
I must note here that to trigger the reload the size of the file must change meaning that if you have made changes to the code that did not influence the size of the file this will not trigger the reload. In this case to force the reload you can, for example, add a space.<br>
As always, if you make a mistake RAICK will propagate an error and put your bot to <i>Safe Mode</i>, from which <code>Quick Reload</code> will not work anymore.