# Fortran Regex
Fortran regex using C++ regex. Wrapped C++ to C. Accessing C functions with Fortran

### Functions:
regex_replace\
regex_match\
regex_search\
regex_match_logical\
regex_contains\
regex_indexof\
regex_indexofend\
regex_lastindexof\
regex_lastindexofend

### Types:
reg_data, r_matches, r_data, reg_matches

## How to:
### Regular Expressions:
The slashes in the regular expressions don't need to be escaped for slashes like in C or C++
### Functions:
All flags are optional\

#### regex_replace:
Replaces different text in the string if it matches the regular expressions. Automatically it is global by default.\
First argument: String\
Second argument: Regular expression string\
Third argument: Replacement string\

It returns a new string with the modifications
```
 regex_replace("I am testing this code out","\w{4,}","Test")
```
#### regex_match:
If the whole string matches the regular expression then matches will return in a string array

First argument: String\
Second argument: Regular expression string\

It returns a new string with the modifications
```
 regex_match("I am testing this code out","\w{4,}")
```
#### regex_search:
If any part of the string matches the regular expression then an array of arrays will return with positions of the match with the match substring itself.

The first match index is the whole match meaning all the captures or non captures combined in a string. THe second capture and others are individual captures that are done with closed parenthesis ( ) in the regular expression.

First argument: String\
Second argument: Regular expression string\

```
 regex_search("I am testing this code out","\w{4,}")
```
Example:
```
  w=regex_search("I am testing this to make sure it works correctly","(\w{4,})")
    do i=1,size(w)
        print *,"match#:",i
        do i2=1,size(w(i)%match)
            print *,"capture#:",i2
            print *,"str:",w(i)%match(i2)%str
            print *,"start:",w(i)%match(i2)%start,"end:",w(i)%match(i2)%end
            print *,""
        end do
    end do
```
Result:
```
match#:           1
 capture#:           1
 str:testing
 start:           6 end:          12
 
 capture#:           2
 str:testing
 start:           6 end:          12
 
 match#:           2
 capture#:           1
 str:this
 start:          14 end:          17
 
 capture#:           2
 str:this
 start:          14 end:          17
 
 match#:           3
 capture#:           1
 str:make
 start:          22 end:          25
 
 capture#:           2
 str:make
 start:          22 end:          25
 
 match#:           4
 capture#:           1
 str:sure
 start:          27 end:          30
 
 capture#:           2
 str:sure
 start:          27 end:          30
 
 match#:           5
 capture#:           1
 str:works
 start:          35 end:          39
 
 capture#:           2
 str:works
 start:          35 end:          39
 
 match#:           6
 capture#:           1
 str:correctly
 start:          41 end:          49
 
 capture#:           2
 str:correctly
 start:          41 end:          49

```

#### regex_match_logical and regex_contains
If a regular expression matches the whole string regex_match_logical will return true. If a regular expression matches part of a string then regex_contains returns true.
First argument: String\
Second argument: Regular expression string\

It returns a new string with the modifications
```
 regex_match_logical("I am testing this code out","\w{4,}")
 regex_contains("I am testing this code out","\w{4,}")
```
#### regex_indexof, regex_indexofend, regex_lastindexof, regex_lastindexofend
These functions return the index which the match is detected. If nothing is found then these functions return -1 meaning nothing was found.
First argument: String
Second argument: Regular expression string

regex_indexof returns the first match occurance starting position
regex_indexofend returns the first match occurance end position
regex_lastindexof returns the last match occurance starting position
regex_lastindexofend returns the last match occurance end position
```
 regex_indexof("I am testing this code out","\w{4,}")
 regex_indexofend("I am testing this code out","\w{4,}")
 regex_lastindexof("I am testing this code out","\w{4,}")
 regex_lastindexofend("I am testing this code out","\w{4,}")
```

### Flags:
The flags are similar to those in C++ regex.

Flag argument variables are: sflags, mflags

They are optional and they are integer arrays. The flags are parameters with integer values. You can mix match them in any order in a array

```
sflags=[r_icase,r_ECMAScript]
mflags=[r_format_first_only,r_match_any]
```

#### sflags: - syntax_option_type
r_icase\
r_nosubs\
r_optimize\
r_collate\
r_ECMAScript\
r_basic\
r_extended\
r_awk\
r_grep\
r_egrep

#### mflags: - match_flag_type
r_match_default\
r_match_not_bol\
r_match_not_eol\
r_match_not_bow\
r_match_not_eow\
r_match_any\
r_match_not_null\
r_match_continuous\
r_match_prev_avail\
r_format_default\
r_format_sed\
r_format_no_copy\
r_format_first_only

Examples with flags:
```
regex_search("I am testing this to make sure it works correctly","(\w{4,})",sflags=[r_icase],mflags=[r_match_any])
regex_search("I am testing this to make sure it works correctly","(\w{4,})",sflags=[r_icase])
regex_search("I am testing this to make sure it works correctly","(\w{4,})",mflags=[r_match_any])
regex_search("I am testing this to make sure it works correctly","(\w{4,})",mflags=[r_match_any],sflags=[r_icase])
```
