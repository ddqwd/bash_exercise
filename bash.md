## Shell Parameter ##

## A parameter can be a name , a number , or one of the spcial characters listed below.
### 3.1.2.4 ANSI_C Quoting ###

```bash
$ echo $'\a'   # Character sequences of the form $' string'
$ echo $'\cc'   # a control-x chacter

```
### Local-Specific Translation ###
```bash

```

### Reserved Words ###
Reserved words are use to begin and end the shell's compound commands.
```bash
$ echo if then elif else fi
$ echo time
$ echo for in until while do done 
$ echo case esac coproc select function
$ echo { } [[ ]] !

# in is recognized as a reserved word if it is the third word of a case or select in and do are recognized as reserved words if they are the third word in a for command
$ if [ "$1" in ("cat", "dog", "moudse") ]; then echo "doola" fi
syntax error 
$ case "$1" in "cat") echo "d";;*) echo "s";; esac

```


### Piplelines ###
```bash
$ lsfd | grep b
$ lsfd |& grep b   # l& is shorthand for 2>&1.
$ time -p lsfd |& grep b  # time print the time once it finishes. -p changes output format to that specified by POSIX
```





### 3.4.1 Positional Parameter ###

** A positional parameter is a parameter denoted by one or more digits, other than the single 0. **
    
```bash
$ set -- a b c d e f g h j k l m n # using the set builtin command reassigned
$ echo $1           # N is only a single digit
$ echo $10          # use braces.

```
### 3.4.2 Special Parameters ###

** Special parameter only be referenced , not allowed to be assigned. ** 
```bash
$ set -- a b c d
$ echo $*              # Expands to the positional parameters, starting from one.
a b c d
$ IFS=,.
$ echo "$*"      # expands to single word with the value of each parameters separated by the first character of the IFS
a,b,c,d
$ unset IFS    # default spaces
$ echo "$*"    
a b c d
$ IFS=         # join the parameters without intervening separators.
$ echo "$*"    
abcd

```

## Shell Parameter Expansion ##


```bash

val=2
echo ${val}   # the basic form of parameter expansion           
$ vall=3
$ echo ${val}l  # also require braces to distinct
2
$ v=123
$ echo ${v-unset}   # only test existence
123
$ v=
$ echo ${v:-unset}  # test existence and null value.
unset
$ echo $v
v
$ : ${v:=DEFAULT}   # if v is unset or null , word is assign to v
$ echo $v
DEFAULT
$ v=
$ : ${v:? v is unset or null}  # if v is unset or null , report the expansion of word
bash v : v is unset or null
$ v=123
echo ${v:+v is set and not null} #  if v is not null or unset , word is substituted.
v is set and not null
$ v=
echo ${v:+v is set and not null}  # nothing  is substituted

$ string=01234567890abcdefgh
$ echo ${string:7} # extending to the end of the value
7890abcdefgt
$ echo ${string:7:2}   # extending up to 2 size
78
$ echo ${string:7:0}   #  extending up to the zerolength

$ echo ${string:-7:2}  # error , must a space before -7
$ echo ${string: -7:2}  # negative offset counts back from the end of the value of parameter.
bc
$ echo ${string: -7:-2}  # negative length counts back from the end of the value of parameter rather than a number of characters.;
bcdef
$ set -- 01234567890abcdefgh
$ echo ${1:7}


```

## Bash Command ##
```bash
$ echo "12:ab" | cut -f 1 -d :
```
