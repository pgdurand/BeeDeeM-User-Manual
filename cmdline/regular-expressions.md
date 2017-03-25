# Using regular expressions in descriptors

[Databank descriptors](/cmdline/descriptors-format.md) (".dsc" files) accept regular expressions in their "db.files.include" and "db.files.exlude" directives.

Here is a short documentation about the accepted expressions.






| :--- | :--- |
| _._ | any character |
| _\d_ | a digit: [0-9] |
| _\D_ | a non-digit: [^0-9] |
| _\w_ | a word character: [a-zA-Z_0-9] |
| _\W_ | a non-word character: [^\w] |

### Special characters