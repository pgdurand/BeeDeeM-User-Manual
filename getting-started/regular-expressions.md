# Appendix - Regular expressions

[Databank descriptors](descriptors-format/) \(".dsc" files\) accept regular expressions in their "db.files.include" and "db.files.exlude" directives.

Here is a short documentation about the accepted expressions.

## Basic concepts

A regular expression, often called a pattern, is an expression that describes a set of strings. They are usually used to give a concise description of a set, without having to list all elements. Alternatively, a pattern can be used to identify strings containing at least one of the possible strings defined by the pattern. In the field of bioinformatics, there is a well-known example of the usage of regular expressions: the Prosite patterns are nothing else than such expressions.

_BeeDeeM_'s descriptor system gives you the opportunity to use regular expressions. In the context of databank descriptors, these expressions are quite useful to specify which files and directories have to be donwloaded or discarded from the remote servers.

## Regular expression syntax

### Very basic expressions

The simplest regular expression is a simple string: A, ATG, kinase, etc.

### Alternation

A vertical bar separates alternatives. For example, gray\|grey, can match gray or grey.

### Grouping

Parentheses are used to define the scope and precedence of the operators. For example, gr\(a\|e\)y, means gr follows by a or e, follows by y. It is equivalent to gray\|grey and can also match gray or grey.

### Case sensitivity

By default, regular expressions are case-sentitive. As a consequence the pattern atg cannot recognize the stringATG.Usingthespecialconstruct\(?i\)allowstosearchforcase-insentitivepatterns.The\(?i\)modifier affects all characters to the right and in the same group, if any. For example in the pattern a\(?i\)tg, only t is allowed to be case-insensitive, whereas in \(?i\)\(atg\) all characters are allowed to be case-insensitive. The pattern \(?i\)\(atg\) can match atg, aTg, ATg, ATG, etc.

### Quantification

A quantifier after a character or group specifies how often consecutive occurrences of that preceding expression are allowed to occur. The available quantifiers are ?, \*, and +.

The question mark indicates there is 0 or 1 of the previous expression. For example, colou?r matches both color and colour.

The asterisk indicates there are 0, 1 or any number of the previous expression. For example, "go\*gle" matches ggle, gogle, google, gooogle, etc.

The plus sign indicates that there is at least 1 occurrence of the previous expression. For example, "go+gle" matches gogle, google, gooogle, etc. \(but not ggle\).

### Extended quantification

The expression {x,y}, where x and y are numbers, can be used to define more precise quantification. For example T{x} means T exactly x times. T{x,} means T at least x times. \(ATG\){x,y} means ATG at least x but not more than y times.

### Character classes

Character classes are defined using \[ and \] to match a single character that is contained within the brackets. For example, \[abc\], matches a, b or c at any given position of a string. Expression  matches any character except a, b, or c \(negation\). Expression \[a-zA-Z\] matches a through z or A through Z, inclusive \(range\).

### Predefined character classes

The following table gives some useful predefined character classes.

| Global task name | arguments |
| :--- | :--- |
| _._ | any character |
| _\d_ | a digit: \[0-9\] |
| _\D_ | a non-digit:  |
| _\w_ | a word character: \[a-zA-Z\_0-9\] |
| _\W_ | a non-word character:  |

### Special characters

^ matches the beginning of a string. $ matches the end of a string. For example, ^\[hc\]at matches hat and cat but only at the beginning of a string, and \[hc\]at$ matches hat and cat but only at the end of a string.

