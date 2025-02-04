# Bash Brackets Quick Reference - 17.02.22


Bash has lots of different kinds of brackets. Like, many much lots. It adds meaning to doubling up different brackets, and a dollar sign in front means something even more different. *And*, the brackets are used differently than many other languages. I constantly find myself doing a 5-second search for which one is the right one to do since I'm not writing Bash scripts all the time. So here, I'm going to lay them all out and then print this article out and staple it to the wall by my desk. Possibly with a decorative frame. So here we go.

A tiny note on all of these is that Bash generally likes to see a space between round or square brackets and whatever's inside. It doesn't like space where curly braces are concerned. We'll go through in order of net total squigglyness (NTS score).

## [( Single Parentheses )](https://dev.to/rpalo/bash-brackets-quick-reference-4eh6#-single-parentheses-)

Single parenthesis will run the commands inside in a **subshell**. This means that they run through all of the commands inside, and then return a single exit code. Any variables declared or environment changes will get cleaned up and disappeared. Because it's within a subshell, if you have it inside a loop, it will run a little slower than if you called the commands *without* the parentheses.  

```
a='This string'
( a=banana; mkdir $a )
echo $a
# => 'This string'
ls
# => ...
# => banana/
```


## [(( Double Parentheses ))](https://dev.to/rpalo/bash-brackets-quick-reference-4eh6#-double-parentheses-)

This is for use in integer arithmetic. You can perform assignments, logical operations, and mathematic operations like multiplication or modulo inside these parentheses. However, do note that there is no output. Any variable changes that happen inside them will stick, but don't expect to be able to assign the result to anything. If the result inside is **non-zero**, it returns a **zero** (success) exit code. If the result inside is **zero**, it returns an exit code of **1**.  

```
i=4
(( i += 3 ))
echo $i
# => 7
(( 4 + 8 ))
# => No Output
echo $?  # Check the exit code of the last command
# => 0
(( 5 - 5 ))
echo $?
# => 1

# Strings inside get considered 'zero'.
(( i += POO ))
echo $i
# => 7

# You can't use it in an expression
a=(( 4 + 1 ))
# => bash: syntax error near unexpected token '('
```


## [<( Angle Parentheses )](https://dev.to/rpalo/bash-brackets-quick-reference-4eh6#lt-angle-parentheses-)

*Thank you to [Thomas H Jones II](https://dev.to/ferricoxide) for this comment that inspired this section on Process Substitution*

This is known as a *process substitution*. It's a lot like a pipe, except you can use it anywhere a command expects a file argument. And you can use multiple at once!  

```
sort -nr -k 5 <( ls -l /bin ) <( ls -l /usr/bin ) <( ls -l /sbin )

# => Like a billion lines of output that contain many of the
# => executables on your computer, sorted in order of descending size.

# Just in case you don't magically remember all bash flags,
# -nr  means sort numerically in reverse (descending) order
# -k 5 means sort by Kolumn 5.  In this case, for `ls -l`, that is the "file size"
```



This works because the sort command expects one or many filenames as arguments. Behind the scenes, the `<( stuff )` actually outputs the name of a temporary file (unnamed pipe file) for the `sort` command to use.

Another example of where this comes in handy is the use of the `comm` command, which spits out the lines that the files have in common. Because `comm` needs its input files to be sorted, you could either do this:  

```
# The lame way
sort file1 > file1.sorted
sort file2 > file2.sorted
comm -12 file1.sorted file2.sorted
```



Ooooor, you can be a total BAshMF and do it this way:  

```
# The baller way
comm -12 <( sort file1 ) <( sort file2 )
```



## [](https://dev.to/rpalo/bash-brackets-quick-reference-4eh6#-dollar-single-parentheses-)$( Dollar Single Parentheses )

This is for interpolating a subshell command output into a string. The command inside gets run inside a subshell, and then any output gets placed into whatever string you're building.  

```
intro="My name is $( whoami )"
echo $intro
# => My name is ryan

# And just to prove that it's a subshell...
a=5
b=$( a=1000; echo $a )
echo $b
# => 1000
echo $a
# => 5
```



## [](https://dev.to/rpalo/bash-brackets-quick-reference-4eh6#-dollar-single-parentheses-dollar-q-)$( Dollar Single Parentheses Dollar Q )$?

*Shoutout again to [Thomas](https://dev.to/ferricoxide/comment/3pdn) for the tip!*

If you want to interpolate a command, but only the exit code and not the value, this is what you use.  

```
if [[ $( grep -q PATTERN FILE )$? ]]
then
  echo "Dat pattern was totally in dat file!"
else
  echo "NOPE."
fi
```



Although, really, this isn't so much a special bracket pattern as it is an interesting use of `$?`, since the above works even if there is a space between the `$( stuff )` and the `$?`. But a neat tip, nonetheless.

## [](https://dev.to/rpalo/bash-brackets-quick-reference-4eh6#-dollar-double-parentheses-)$(( Dollar Double Parentheses ))

Remember how regular **(( Double Parentheses ))** don't output anything? Remember how that is# Bash Brackets Quick Reference - 17.02.22

 kind of annoying? Well, you can use **$(( Dollar Double Parentheses ))** to perform an **Arithmetic Interpolation**, which is just a fancy way of saying, "Place the output result into this string."  

```
a=$(( 16 + 2 ))
message="I don't want to brag, but I have like $(( a / 2 )) friends."
echo $message
# => I don't want to brag, but I have like 9 friends."

b=$(( a *= 2 ))         # You can even do assignments.  The last value calculated will be the output.
echo $b
# => 36
echo $a
# => 36
```



One thing to remember is that this is strictly integer arithmetic. No decimals. Look into [`bc`](https://www.lifewire.com/use-the-bc-calculator-in-scripts-2200588) for floating point calculations.  

```
echo $(( 9 / 2 ))  # You might expect 4.5
# => 4

echo $(( 9 / 2.5 ))
# => bash: 9 / 2.5 : syntax error: invalid arithmetic operator (error token is ".5 ")
```



## [](https://dev.to/rpalo/bash-brackets-quick-reference-4eh6#-single-square-brackets-)\[ Single Square Brackets \]

This is an alternate version of the built-in `test`. The commands inside are run and checked for "truthiness." Strings of zero length are false. Strings of length one or more (even if those characters are whitespace) are true.

[Here are a list of all of the file-related tests you could do](http://tldp.org/LDP/abs/html/fto.html), like checking if a file exists or if it's a directory.

[Here are a list of all of the string-related and integer-related tests you could do](https://www.tldp.org/LDP/abs/html/comparison-ops.html), like checking if two strings are equal or if one is zero-length, or if one number is bigger than another.  

```
if [ -f my_friends.txt ]
then
    echo "I'm so loved!"
else
    echo "I'm so alone."
fi
```



One last thing that's important to note is that `test` and `[` are actually shell commands. `[[ ]]` is actually *part of the shell language itself*. What this means is that the stuff inside of Double Square Brackets isn't treated like arguments. The reason you would use Single Square Brackets is if you need to do *word splitting* or *filename expansion*.

Here's an illustration of the difference. Let's say you used Double Square Brackets in the following way.  

```
[[ -f *.txt ]]
echo $?
# => 1
```



False, there is no file explicitly named "\[asterisk\].txt". Let's assume there are currently no `.txt` files in our directory.  

```
# If there's no files .txt files:
[ -f *.txt ]; echo $?
# => 1
```



`*.txt` gets expanded to a blank string, which is not a file, and *then* the test gets evaluated. Let's create a txt file.  

```
touch cool_beans.txt
# Now there's exactly one .txt file
[ -f *.txt ]; echo $?
# => 0
```



`*.txt` gets expanded to a space-separated list of matching filenames: "cool\_beans.txt", and then the test gets evaluated with that one argument. Since the file exists, the test passes. But what if there's two files?  

```
touch i_smell_trouble.txt  # bean pun.  #sorrynotsorry
# Now there's two files
[ -f *.txt ]
# => bash: [: too many arguments.
```



`*.txt` gets expanded to "cool\_beans.txt i\_smell\_trouble.txt", and then the test is evaluated. Bash counts each of the filenames as an argument, receives 3 arguments instead of the two it was expecting, and blurffs.

Just to hammer my point home: even though there are currently two `.txt` files, this next test still fails.  

```
[[ -f *.txt ]]; echo $?
# => 1.  There is still no file called *.txt
```



I tried to come up with some examples of why you would want this, but I couldn't come up with realistic ones.

> For the most part, it seems like, a good rule of thumb is: if you need to use `test` or `[ ]`, you'll know it. If you're not sure if you need it, you probably don't need it and you should probably use **\[\[ double square brackets \]\]** to avoid a lot of the tricky gotchas of the `test` command. If your shell is modern enough to have them.

## [](https://dev.to/rpalo/bash-brackets-quick-reference-4eh6#-double-square-brackets-)\[\[ Double Square Brackets \]\]

True/false testing. Read through the section above for an explanation of the differences between single and double square brackets. Additionally, double square brackets support extended regular expression matching. Use quotes around the second argument to force a raw match instead of a regex match.  

```
pie=good
[[ $pie =~ d ]]; echo $?
# => 0, it matches the regex!

[[ $pie =~ [aeiou]d ]]; echo $?
# => 0, still matches

[[ $pie =~ [aei]d ]]; echo $?
# => 1, no match

[[ $pie =~ "[aeiou]d" ]]; echo $?
# => 1, no match because there's no literal '[aeoiu]d' inside the word "good"
```



Also, inside double square brackets, `<` and `>` sort by your locale. Inside single square brackets, it's by your machine's sorting order, which is usually ASCII.

## [](https://dev.to/rpalo/bash-brackets-quick-reference-4eh6#-single-curly-braces-){ Single Curly Braces }

Single curly braces are used for expansion.  

```
echo h{a,e,i,o,u}p
# => hap hep hip hop hup
echo "I am "{cool,great,awesome}
# => I am cool I am great I am awesome

mv friends.txt{,.bak}
# => braces are expanded first, so the command is `mv friends.txt friends.txt.bak`
```



The cool thing is that you can make ranges as well! With leading zeros!  

```
echo {01..10}
01 02 03 04 05 06 07 08 09 10
echo {01..10..3}
01 04 07 10
```



## [](https://dev.to/rpalo/bash-brackets-quick-reference-4eh6#dollar-braces)${dollar braces}

Note that there are no spaces around the contents. This is for variable interpolation. You use it when normal string interpolation could get weird  

```
# I want to say 'bananaification'
fruit=banana
echo $fruitification
# => "" No output, because $fruitification is not a variable.
echo ${fruit}ification
# => bananaification
```



The other thing you can use **${Dollar Braces}** for is variable manipulation. Here are a few common uses.

Using a default value if the variable isn't defined.  

```
function hello() {
  echo "Hello, ${1:-World}!"
}
hello Ryan
# => Hello Ryan!
hello
# => Hello World!

function sign_in() {
    name=$1
  echo "Signing in as ${name:-$( whoami )}"
}
sign_in
# => Signing in as ryan
sign_in coolguy
# => Signing in as coolguy
```



Getting the length of a variable.  

```
name="Ryan"
echo "Your name is ${#name} letters long!"
# => Your name is 4 letters long!
```



Chopping off pieces that match a pattern.  

```
url=https://assertnotmagic.com/about
echo ${url#*/}     # Remove from the front, matching the pattern */, non-greedy
# => /assertnotmagic.com/about
echo ${url##*/}    # Same, but greedy
# => about
echo ${url%/*}     # Remove from the back, matching the pattern /*, non-greedy
# => https://assertnotmagic.com
echo ${url%%/*}    # Same, but greedy
# => https:
```



*Thanks [Sanket Patel](https://dev.to/sanketjpatel) for the error fix!*

You can uppercase matching letters!  

```
echo ${url^^a}
# => https://AssertnotmAgic.com/About
```



You can get slices of strings.  

```
echo ${url:2:5}  # the pattern is ${var:start:len}.  Start is zero-based.
# => tps://
```



You can replace patterns.  

```
echo ${url/https/ftp}
# => ftp://assertnotmagic.com

# Use a double slash for the first slash to do a global replace
echo ${url//[aeiou]/X}
# => https://XssXrtnXtmXgXc.cXm
```



And, you can use variables indirectly *as the name of other variables*.  

```
function grades() {
  name=$1
  alice=A
  beth=B
  charles=C
  doofus=D
  echo ${!name}
}

grades alice
# => A
grades doofus
# => D
grades "Valoth the Unforgiving"
# => bash: : bad substitution.   
# There is no variable called Valoth the Unforgiving,
# so it defaults to a blank value.  
# Then, bash looks for a variable with a name of "" and errors out.
```



## [](https://dev.to/rpalo/bash-brackets-quick-reference-4eh6#ltltdouble-angle-heredocs)<<Double Angle Heredocs

This is how you make multiline strings in Bash (one method). Two arrows and then a word -- any word that you choose -- to signal the start of the string. The string doesn’t end until you repeat your magic word.  

```
read -r -d '' nice_message <<MESSAGE
Hi there!  I really like the way you look
when you are teaching newbies things
with empathy and compassion!
You rock!
MESSAGE

echo "$nice_message"
# => Hi there!  I really like the way you look
# => when you are teaching newbies things
# => with empathy and compassion!
# => You rock!

# Note, if you store a string with newlines in a variable, 
# you have to quote it to get the newlines to actually print.
# If you just use `echo $nice_message`, it won't reflect newlines.
```



The word can be whatever you want. I generally end up using "HEREDOC" to make it easier for future me.

The real ancient wisdom in the comments section from Ian Kirker:

One final trick is that, if you add a dash after the arrows, it suppresses any leading tabs (*but not spaces*) in your heredoc.  

```
cat <<-HEREDOC
        two leading tabs
    one leading tab
  two spaces here
HEREDOC

# => two leading tabs
# => one leading tab
# =>   two spaces here
```



## [](https://dev.to/rpalo/bash-brackets-quick-reference-4eh6#punctuations-a-killer)Punctuation's a Killer

Hopefully this is helpful. If you see something I missed or have another cool use for one of these variants, be sure to let me know, and I'll update it and publicly praise your genius. Thanks for reading!