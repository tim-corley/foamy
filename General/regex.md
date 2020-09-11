# Regular Expressions

### grep

- `$ grep <Search Term> path/to/file.txt`

```
➜  RegEx grep Beautiful zen.txt
Beautiful is better than ugly.
➜  RegEx grep beautiful zen.txt
➜  RegEx grep -i beautiful zen.txt
Beautiful is better than ugly.
➜  RegEx grep -o Beautiful zen.txt
Beautiful
```

- use `^` to match pattern at beginning of a line:

```
➜  RegEx grep ^If zen.txt
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
```

- use `$` to match pattern at end of line:

```
➜  RegEx grep idea.$ zen.txt
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
```

- match multiple characters:

```
➜  RegEx echo Two too | grep -i 't[ow]o'
Two too
```

- match digits

```
➜  RegEx echo 123 hey 56 hello. | grep -P '\d'
123 hey 56 hello.
➜  RegEx echo 123 hey 56 hello. | grep '[0-9]'
123 hey 56 hello.
```

- repitition - use an `*` to match the preceding item zero or more times

```
➜  RegEx echo two twoo not too twooo. | grep -o 'two*'
two
twoo
twooo
```

a period matches any character. so using: `.*` will match everything between some specified characters

```
➜  RegEx echo __hello__there | grep -o '__.*__'
__hello__
```

the asterisk is **greedy** - will to make as many matches as possible...

```
➜  RegEx echo start__hi__bye__hi__bye-end | grep -o '__.*__'
__hi__bye__hi__
```
