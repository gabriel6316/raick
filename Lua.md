# <font color='#003366'>Lua and the ABC of Programming</font> #
Now, this is not a guide on programming. This is just the basic knowledge that will help you understand how RAICK works. It is mainly theoretical stuff, which may seem too abstracted from the actual AI, but be patient- you must have a strong foundation before we dig into the real thing.
## <font color='#006666'>Client & Script</font> ##
As you probably already know from your experience with AI's the entry point for any AI script is the `AI.lua` / `AI_M.lua` file. This is a regular text file, using which your Ragnarok game client makes(every time your homunculus/mercenary enters the screen) a small program(the AI) that(every time it is called/asked) tells the client what actions should your homunculus/mercenary perform based on the data that the client provides it with. This happens multiple times per second and that's how the AI actually works. When your homunculus/mercenary leaves the screen for some reason(death, _Rest/Vaporize_ skill etc) the AI program is stopped and thrown away with all of its data. Once the the homunculus/mercenary will appear on the screen again the client will make a fresh AI program from the AI text file and the cycle will continue.<br>
So, let's review:<br>
<ul><li>The script text file is loaded only when the bot re-enters the screen(respawnes)<br>
</li><li>The client works with the program(which it made during respawn), not with the text file itself<br>
</li><li>The script text file is not used by the client the rest of the time(you can delete and modify it without any harm)<br>
</li><li>The data that the client gives to the AI to make a decision is static(it is a frozen moment in time and no matter how many times you query it, it will not change during the same call of the AI program)<br>
</li><li>The AI looses all of its data when it stops working<br>
These facts may seem a bit confusing right now, but they will help you to understand some things better in future chapters.<br>
<h2><font color='#006666'>Building blocks of Lua</font></h2>
Let's focus more on that text file. The client assumes it is written in Lua. Being above all a <b>programming language</b> it follows some basic concepts that I would like to explain to you.<br>
<h3><font color='#006600'>Types, Values & Variables</font></h3>
All programming languages have three basic concepts in common:<br>
</li><li>Types<br>
</li><li>Values<br>
</li><li>Variables<br>
And they are a lot simpler than they sound.</li></ul>

<b>Types</b> are used to categorize data. For example, in Lua:<br>
<ul><li><code>1, 42309483209.3129083219038, -9999999999999999</code> are all of type <i>number</i>
</li><li><code>"this is a message"</code> and <code>'this is another message'</code> are of type <i>string</i>(a message consisting of characters)<br>
The number of types that come with the language are often quite limited, but they are very versatile and using them you can define your own ones.<br>
<br>
Now, what about <b>values</b>? Well, actually, you have already seen them! Values are individual elements of types. We can rewrite our example this way:<br>
</li><li><code>1, 42309483209.3129083219038, -9999999999999999</code> are <b>values</b> of type <i>number</i>
</li><li><code>"this is a message"</code> and <code>'this is another message'</code> are <b>values</b> of type <i>string</i>(a message consisting of characters)<br>
Quite simple isn't it? The whole story comes down to this:<br>
</li><li>We have numeric values like: 1, 2, -300 or 123.123, so we define a <i>number</i> type for them. This generalization is very useful to us, since all numbers have many thing in common, for example: we can add them, multiply by one another and they all don't like to be divided by zero.<br>
</li><li>We have message values like: <code>'blah blah blah'</code> or <code>"yep yep yep"</code>, so we define a <i>string</i> type for them. And again it is useful, since we can, for example: "glue" 2 strings together or check how many characters they have.</li></ul>

So, to summarize. Types are names for sets of data(values) with common properties. They define rules to manipulate with the particular piece of data. If we know the type of the value, then we know what we can do with it and what we can't.<br>
<br><br>
Suppose we have our values, which we have divided into groups(types). The obvious question is: where do we store them? And here is when <b>variables</b> enter the scene to help us out. They are just "boxes" with names, where you can store any value of any data type you like. This way you can transfer data between different parts of your script.<br>
<br>
The last thing you need to know is that there are two kinds of variables: <b>local</b> and <b>global</b>. Global ones(as their name suggests) could be used in every part of your script- they are visible everywhere. As for local ones, they are visible only in a small area. Nothing will stop you from using <u>only</u> global variables in your script. Using local ones just helps to keep the global namespace clean. Examples:<br>
<pre><code><br>
a = 1 -- Putting 1 to variable 'a'.<br>
b = 2 + 3 -- Adding two numbers and writing result to 'b'.<br>
a = b - 2.5 -- Here we take the value from the variable 'b' and subtract 2.5 from it. Then we replace 1 in variable 'a' with this result.<br>
a = a * 5 -- And here we multiply the value in the variable by 5.<br>
<br>
--[[<br>
There are certain rules for naming variables. The name can contain letters, numbers and underscores(_), but cannot start with a number. For example:<br>
____a____ is a valid name<br>
_123 is a valid name<br>
123abc is not a valid name<br>
abc$$$ is not a valid name<br>
--]]<br>
<br>
str1 = "a string" -- Typically, we define a string between double quotes, ..<br>
str2 = 'another string' -- .. but single quotes are also permitted.<br>
str3 = str1 .. str2 -- Operator '..' allows us to "glue"(concatenate) two strings together. The result is: "a stringanother string".<br>
</code></pre>
Oh, and one more thing- comments. You put those after <code>--</code> or between <code>--[[</code> and <code>--]]</code>. They are used, when you want to explain certain parts of your code.<br><br>
<hr />
<h3><font color='#006600'>Functions</font></h3>
First of all, the <b>function</b> is a special type. The values that this type represent are individual functions that you define or that come with the Lua language.<br>
Functions are the ones that make something work in your AI. Every piece of code in Lua is executed inside some function. The AI script is also written inside a function, which you should put in a variable <code>AI</code>. This name is an agreement between the client and your script, so that the client knows what function to call after it makes the AI program.<br>
So, as I said, this function contains your whole AI. Of course, it would be hard to make such complex AI's like RampageAI or MirAI with all of the code being in one place. Thus, when you write your AI you usually divide it into different pieces for easier management.<br>
Another good use for functions is when you have a piece of code that you use many times in your script. You could put this code inside a function and call this function every time you need it. A good example from the default AI is the function to calculate the distance between the 2 objects. It receives (x,y) coordinates of those objects and returns the distance between them. Having this function you could call it every time you want to know the distance between some objects without the need to write the same code over and over again.<br>
<br>
Now, you may have noticed something new about functions from the previous paragraph and you are right! Functions can receive values, which are called <b>arguments</b> and can return values. Using arguments you can influence the behavior of the function and/or it's return values. The most trivial example of this concept are the operators(<code>+, -, *, /</code>). They are also functions with a bit different appearance, which take 2 arguments and return a value based on them.<br>
<br>
So, to sum up, we use functions to divide the logic of the script into different parts for easier management or to generalize our code, eliminating the need to write the same thing many times. Examples:<br>
<pre><code><br>
-- This is a function definition. It terms of Lua this means that we put a value of type function into a global variable 'checkForCommands'.<br>
-- The variable is global since we have not told in any way that we refer to a local variable.<br>
-- For now, I don't want you to think too much about those local variables and we'll assume that all our variables are global.<br>
function    checkForCommands()<br>
<br>
-- We do something here.<br>
end<br>
<br>
-- This is a function, which takes 2 arguments and returns their sum.<br>
function    sum2(a, b)<br>
<br>
return a + b<br>
end<br>
<br>
-- This function return the doubled value of it's argument.<br>
function    multiplyBy2(a)<br>
<br>
return a * 2<br>
end<br>
<br>
-- The client calls this function. We just have to define it.<br>
function    AI()<br>
<br>
-- Once the client calls the function it will start one by one doing things that are defined inside.<br>
checkForCommands() -- First of all this, ..<br>
<br>
local sum = sum2(1, 2) -- .. then this ..<br>
<br>
multiplyBy2(sum) -- .. and finally this.<br>
-- You can see that we use a local variable here to store the result of the sum. After the 'AI' function ends this variable will disappear.<br>
-- We could have used the global variable instead, but this way the would "pollute" the global namespace with unneeded data.<br>
end<br>
</code></pre><br><br>
<hr />
<h3><font color='#006600'>Tables</font></h3>
The next interesting type, which is vital for us to fully understand programming in Lua is the <b>table</b>. This is nothing more than a storage for other types(including the table itself). Tables are very versatile and could be used for all kinds of purposes, but you don't need to know much about the complex stuff. What you need to know is that you can put any data you like into the table and retrieve it afterwards. It is very similar to variables, only you are not limited to associating names with your values. In case of tables you can associate any value(which is called <i>key</i>) with any value(which is called just <i>value</i>). Examples:<br>
<pre><code><br>
a = {} -- '{}' is a table constructor. This means that it is a command to create a new table.<br>
<br>
a[1] = 25 -- We put 25 under numeric key 1.<br>
b = a[1] -- We can then retrieve this value by it's key.<br>
<br>
a["abc"] = 12 -- We put 12 under string key "abc"<br>
c = a["abc"] -- We can retrieve this value as always, but ..<br>
d = a.abc -- .. with strings you can also use the dot syntax!<br>
<br>
-- Now watch closely here:<br>
function    a.method(arg)<br>
<br>
return arg<br>
end<br>
<br>
e = a.method(1) -- 'e' now holds value 1.<br>
-- What you see above is a definition of a function inside a table.<br>
-- Technically speaking: I have created a function and put it under string key "method" of a table inside a global variable 'a'.<br>
-- The syntax 'something.something(arg1, arg2, ...)' is very widespread in modern programming languages. What does it mean?<br>
-- Well, be patient, I will certainly refer to it many times in the chapter about using RAICK.<br>
</code></pre><br><br>
<hr />
<h3><font color='#006600'>nil</font></h3>
Before we continue I would like to say a few words about one important type, which is <b>nil</b>. This is a special type, which has only one value- <code>nil</code>. This value specifies the absence of any other value. For example, if you refer to a variable that you have not used before it will contain <code>nil</code>. You can also use <code>nil</code> to delete anything from a variable or from under a table key.<br><br>
<hr />
<h3><font color='#006600'>Conditions & Booleans</font></h3>
So far we have seen programming as a process of writing lines of code that get executed inside some main function, which is being initially called by someone(in our case- the Ragnarok client). What if we want to execute a certain line only when a certain condition is satisfied? We need a way to define conditions and some structure that would interpret them. This structure is known in programming as the <b>if statement</b>. It takes a condition, which can return either <code>true</code> or <code>false</code> and executes the enclosed code based on this value. Now, hold on a second! <code>true</code> or <code>false</code>? What's that? Well, those are values of type <b>boolean</b>. This type has only those 2 values. They are used in cases where you need to know if the result is: positive or negative, yes or no, on or off, true or false etc. That's why they are ideal for <b>conditional expressions</b>. Those are expressions similar to arithmetic ones like <code>2 * 3 + 5</code>, only they deal with logical and comparison operators and return <code>true</code> or <code>false</code> instead of a numeric result. Let's make things clear using examples:<br>
<pre><code><br>
a = 1<br>
b = 2<br>
<br>
-- We check if the sum of 'a' and 'b' is less than 5 then we execute the code inside the if statement<br>
if (a + b) &lt; 5 then<br>
c = 10<br>
end<br>
<br>
--[[<br>
There are 6 types of comparison operators:<br>
&lt; - less<br>
&gt; - greater<br>
&lt;= - less or equals<br>
&gt;= - greater or equals<br>
== - equals<br>
~= - not equals<br>
<br>
First 4 of them can be used to compare numbers and strings(they are compared by alphabetic order) only.<br>
The last 2 can be used to compare any type with any type.<br>
Note: String '123' is not equal to number 123.<br>
--]]<br>
<br>
c = "abc"<br>
d = 8<br>
e = 3<br>
<br>
-- Here we use logical operators(or, and, not) to combine small conditions into a big conditional expression.<br>
if (c == "cba") or ((d &gt; 6) and (e == 3)) then<br>
-- 'c' is not equal to "cba", 'd' is greater than 6, 'e' equals 3.<br>
-- We get: false or (true and true). Operator 'and' returns true if both arguments are true.<br>
-- 'or' returns true if at least one argument is true.<br>
-- So we get: false or true -&gt; true.<br>
-- The whole statement is true and code inside 'if' will be executed.<br>
if not(b ~= 2) then<br>
-- 'not' just returns the opposite.<br>
-- b is indeed 2, so b ~= 2 returns false and 'not' makes it true, so the whole statement is true and code inside 'if' will be executed.<br>
h = 4<br>
end<br>
end<br>
<br>
--[[<br>
There are 3 logical operators available:<br>
and - Returns true if both arguments are true. false otherwise.<br>
or - Returns true if at least one argument is true. false otherwise.<br>
not - Returns true if the argument is false. false otherwise.<br>
--]]<br>
<br>
a = true<br>
b = nil<br>
c = 1<br>
<br>
-- We can use the values themselves as conditional expressions. Everything other than 'nil' and 'false' with be turned to true.<br>
if a then -- 'a' is already true, so the code inside if will be executed<br>
-- 'b' is nil so it turns to false. 'c' is 1, which is neither nil nor false, so it becomes true. false and true -&gt; false, so the if won't be executed.<br>
if b and c then<br>
a = 2<br>
end<br>
<br>
b = 1<br>
end<br>
<br>
-- 'If' can also be paired with 'else' or 'elseif'.<br>
if b then -- false<br>
d = 1<br>
elseif not a then -- false<br>
d = 2<br>
elseif c then -- true!<br>
d = 3<br>
elseif a and not b then -- not checked<br>
d = 4<br>
else<br>
d = 5<br>
end<br>
-- If's are checked one by one until one of them receives true and if this does not happen, then the code inside 'else' will be executed.<br>
-- In this example d will get 3.<br>
</code></pre><br><br>
<hr />
<h3><font color='#006600'>Loops</font></h3>
The final structure you need to know about is the <b>loop</b>. This structure is very similar to the if statement, only in this case the code gets executed over and over again while the conditional expression is <code>true</code>. There are many types of loops in Lua, but with RAICK you will actually need to know only one of them- the <b>for</b> loop. This loop has 2 ways of using it. Let's examine both of them in the following example:<br>
<pre><code><br>
a = 0<br>
<br>
-- This is the first way to use this loop. First of all you need to define some local variable that will hold the current index(in our case it is variable 'i').<br>
-- Then you define the starting number(1 in this example) and the ending number(100).<br>
-- With every cycle of the loop the value in 'i' will grow by 1 until it reaches 100. And every time the 'i' grows the code inside the loop gets executed.<br>
-- Note: 'i' is a regular variable like any other. You can use it inside the loop and even change it.<br>
for i = 1, 100 do<br>
a = a + 2<br>
end<br>
-- 'a' is now 200<br>
<br>
b = {}<br>
b[1] = 2<br>
b[2] = 5<br>
b[3] = -2<br>
<br>
c = 0<br>
<br>
-- This is probably the main loop, which you will be using in RAICK, ..<br>
-- .. since it allows searching through sets of data like friend lists, target lists or the list of monsters, players and NPC's on the screen.<br>
-- It has a bit more complex logic behind it, but I will tell you only the stuff that you need to know.<br>
-- In the example below between 'in' and 'do' you see a function, which takes a table 'b' as an argument.<br>
-- This is a function from the Lua standard library(be patient, this will be covered in the next section), ..<br>
-- .. which assumes that the given table has all of it's values under numeric keys starting from 1.<br>
-- Knowing that it then starts passing one by one values from the table to the for loop.<br>
-- The key from the table is written to the first variable of the loop('i' in our example) and the value to the second one('v').<br>
-- The code inside the loop is executed as many times as there are sequential values in the table ..<br>
-- .. (meaning that if the table has values under keys 1, 2, 4, 5, 8 only 1, 2 will be used in the loop, because at number 3 it will assume that the list has ended).<br>
for i, v in ipairs(b) do<br>
c = c + v<br>
end<br>
-- 'c' is now 5<br>
<br>
-- One last thing:<br>
g = 0<br>
<br>
for i = 1, 100 do<br>
g = g + 1<br>
<br>
if g &gt; 50 then<br>
break<br>
end<br>
end<br>
-- The 'break' statement can be used inside the loop to stop it anytime you like.<br>
-- 'g' is now 51.<br>
</code></pre><br><br>
<hr />
<h3><font color='#006600'>Standard Libraries</font></h3>
A <b>standard library</b> is nothing more than a set of predefined functions that come with the language. Mathematical operators(<code>+, -, /, *</code>) are good examples of such functions, but there are a lot more. You have already seen the <code>ipairs</code> function, that can help us to search through a table, which is organized into a primitive list. The next very important function in context of RAICK is <code>require</code>. With it's help you can divide your script into multiple files and link them to your main file like so:<br>
<pre><code><br>
require "./AI/USER_AI/RAICK.lua" -- This is also how you attach RAICK to the AI.lua/AI_M.lua.<br>
</code></pre>
Sometimes you need to know what type is the given value. It this case <code>type</code> function is very useful. It returns the name of the type in form of a string. For example:<br>
<pre><code><br>
a = 1<br>
b = "abc"<br>
c = false<br>
function    d()<br>
end<br>
<br>
type(a) -- returns "number"<br>
type(b) -- returns "string"<br>
type(c) -- returns "boolean"<br>
type(d) -- returns "function"<br>
type(e) -- returns "nil", because 'e' has not been used<br>
</code></pre>
Another useful function is <code>math.random</code>. It takes 2 numeric(can be negative) arguments and returns a random number between them:<br>
<pre><code><br>
rand = math.random(-3, 2) -- Returns -3, -2, -1, 0, 1 or 2 randomly.<br>
</code></pre>
Random is often useful in programming. The main use for it in AI scripts is the, so called, "dance attack".<br>
These are just some examples of standard functions. This is just a short overview of Lua, so I am not doing to cover the rest of them(and they are quite useless for you anyway).<br><br>
<hr />
<h3><font color='#006600'>The Hard Part: Objects and Primitive Types</font></h3>
OK, we are almost done! I don't know if this is actually the hardest part, but it tends to be quite confusing for most people. I just want you to try to understand it, since it is a very important issue, especially with RAICK.<br>
Let's, first of all, review what types we have learned during this quick guide:<br>
<ul><li>number<br>
</li><li>string<br>
</li><li>boolean<br>
</li><li>nil<br>
</li><li>function<br>
</li><li>table</li></ul>

These types are all you will need for your script. Every AI, every script and even RAICK, they all use only those types and not a type more. Now, you might have noticed that to create the first 4 of them you don't need to do anything special. You just write the value you need and it is there. For the rest 2 of them you have a bit more specific ways. If you remember I have mentioned the word <i>constructor</i> somewhere in the section about tables. Well, you can say that both the table and the function have constructors to create them. Let me demonstrate this with an example:<br>
<pre><code><br>
a = {} -- '{}' is a table constructor.<br>
<br>
-- Here we create a function and place it in the variable 'b', which ..<br>
function    b(arg1, arg2)<br>
end<br>
<br>
-- .. is basically identical to writing the following:<br>
b = function(arg1, arg2)<br>
end<br>
-- Or this:<br>
b = function(arg1, arg2) end<br>
-- You can see that 'function() ... end' is nothing more than function constructor.<br>
</code></pre>
In Lua those types that don't have any special ways to define their values are called <b>primitive types</b> and the other ones are called <b>objects</b>. This is not the only difference between those two groups and, in fact, not the main one. The main difference is in the way they are stored in variables. Primitive types are stored <b>by value</b> and objects are stored <b>by reference</b>. It is not easy for a beginner to understand this significant difference, but, nevertheless I will try to make it clearer:<br>
<pre><code><br>
-- Suppose we have put a number into a variable:<br>
a = 1<br>
-- This is a primitive type, which means that the value itself is stored in the variable.<br>
-- What this means is that when we query/read what is stored in the variable we get a copy of the value:<br>
b = a -- 'b' now holds a copy of what is stored in 'a'- number 1.<br>
<br>
type(a) -- A copy of the value in 'a' is passed as an argument, not the value itself.<br>
-- The value in 'a' and the value that will be processed inside the function are 2 different exemplars of the same value.<br>
<br>
-- Let's now see how the object behaves.<br>
a = {}<br>
-- 'a' holds a reference(think of a hyperlink in your browser) to the table, which has been created using constructor '{}'.<br>
-- When we query what is stored in the variable we get a copy of the reference(not the value)- a copy of the link to the same value:<br>
b = a<br>
-- Now both 'a' and 'b' hold links to the same value.<br>
-- If you modify the table through the variable 'a' these changes will also be visible through variable 'b', since they both refer to the same value.<br>
a.abc = 1<br>
<br>
c = b.abc -- You will get 1, since the table has been modified before.<br>
-- It does not matter which variable you use to modify the table or query from it- the result is identical.<br>
<br>
-- Let's do the same thing with a function:<br>
function    a()<br>
<br>
return 1<br>
end<br>
<br>
b = a<br>
-- Both 'a' and 'b' now refer to the same function.<br>
-- It does not matter if a call a function using 'a' or 'b'- in both cases the same function will be called returning number 1.<br>
<br>
c = a()<br>
d = b()<br>
-- Both 'c' and 'd' now contain 1.<br>
</code></pre>
With references you need to be more careful, since, for example, if you pass the table as an argument to a function, you will pass not the copy of the value, but the reference to value itself. Any modifications that the function will perform will be on the given table, not on it's copy. The good news, however, is that references give us a lot of interesting possibilities that the primitive types don't have. For example, references to self:<br>
<pre><code><br>
-- Suppose we have a table:<br>
a = {}<br>
-- Remember that we can put any type of value inside a table, even another table and now we know that the table is stored as a reference.<br>
a.a = a -- We can put a reference to a table under some key of the same table. In this case under string key 'a'.<br>
-- Now, when we will query what is stored under that key we will get the same table back:<br>
b = a.a -- 'b' now holds reference to the same table as 'a'.<br>
-- So we can query it again:<br>
b = a.a.a<br>
-- And again:<br>
b = a.a.a.a<br>
-- And so on:<br>
b = a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a.a<br>
-- And we'll still get our table back.<br>
</code></pre>
This is just a funny example, but this principle actually has a great implementation in RAICK as you will see later.<br>
I hope that I have made this important issue a bit less complicated. Try to understand it, since in RAICK you will mainly be dealing with objects.<br><br>
<hr />
<h3><font color='#006600'>It's Over!</font></h3>
Finally! Your torture is over! We have covered the most boring and most crucial part of mastering RAICK. Now, you have the knowledge to dig into the interesting part- <a href='GettingStarted.md'>a quick guide on using RAICK</a>.