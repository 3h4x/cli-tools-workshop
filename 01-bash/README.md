# Bash

bash (Bourne-again shell) is a unix shell and command language

## Variables
### Builtin variables

`$?` - return code of command  
`$0` - script name  
`$1 - $9` - first 9 arguments passed to script  
`$@` - all arguments passed to script  
`$RANDOM` - random number  
`$SECONDS` - number of seconds since script has started  
`$LINENO` - number of current executed line in a script

### Using variables

Set variable by simple assigning a value to it. After doing this it will be available in context of current shell.  

You can print variable by just using `echo` with or without `"`. Remember that `'` is preventing variable expansion.  
```bash
MESSAGE='Print me!'
echo $MESSAGE  
echo "$MESSAGE"
echo '$MESSAGE'
```

It's a best practice to always use `{}` around bash variable to prevent not expanding variable gotcha.   
```bash
TEST_PATH='/path'
echo "$TEST_PATH_my_file"  
echo "${TEST_PATH}_my_file"  
```

#### Variable modification - advanced

For commands below we do have variable `TEST='/test/variable/path/file.json'` in current shell context

- **Get length of string `${#VAR}`**

    ```bash
    echo ${#TEST}
    ```
    Output: `29`

- **Remove pattern from variable starting from left side `${VAR#pattern}`**

    Remove string `/` from variable. 
    ```bash
    echo ${TEST#/}
    ```
    Output: `test/variable/path/file.json`

- **Remove longest pattern from variable starting from left side `${VAR##pattern}`**

    Greedy remove string `/` from variable. 
    ```bash
    echo ${TEST##/}
    ```
    Output: `file.json`

- **Remove pattern from variable starting from right side `${VAR%pattern}`**

    Remove file extension `.json` from variable. 
    ```bash
    echo ${TEST%.json}
    ```
    Output: `/test/variable/path/file`

- **Variable substitution `${VAR/search/replace}`**

    Substitute `json` with `csv`
    ```bash
    echo ${TEST/json/csv}
    ```
    Output: `/test/variable/path/file.csv`

- **Get only substring `${VAR:offset:length}`**

    ```bash
    echo ${TEST:20}
    ```
    Output: `file.csv`

    ```bash
    echo ${TEST:20:4}
    ```
    Output: `file`

## Executing commands

### Sequenced


- `command1; command2`  

    `command1` will run and after it finish `command2` will run. `command1`   doesn't have to finish successfully.

    Examples:  
    `echo start; echo end`   
    will print `start` and `end` in new line
     
    `false; echo $?`  
    will print `1` but such commands will have return code 0 

- `command1 || command2`

    `command2` will run only if `command1` has failed (exit code != 0)

    `false || echo "This will be printed"`
    `true || echo "This will not be printed"`

- `command1 && command2`
    `command2` will run only if `command1` has succeeded (exit code == 0)

    `true && echo "This will be printed"`
    `false && echo "This will not be printed"`


### Background

To send command to background you need to add `&` at the end.

```bash
sleep 3600&
```
Output: `[1] 88853`

This means that you have 1 job in background with pid 88853. If you run `sleep 3600&` again you will see `[2] another_pid` which means that you have now 2 jobs in background. You can list them with `jobs` command.  


```bash
sleep 3600&
fg %1
ctrl-z
bg %1
```

Here we create job running in background and then we are bringing it back to foreground with `fg %1` (`%1` is way to get first job). `ctrl-z` will suspend jobs running and we will return to shell. To run our task again in background use `bg %1`.

### Brace expansion

Bash grants you ability to create alternative combinations. It's possible to create lists which can be used as commands input or in scripts.

Imagine you have directory with many files in different formats but you only want to list `.jpg` and `.png`.  
```bash
ls *.{jpg,png}
```

Create list of integers from 1 to 10
```bash
echo {1..10}
```

Create list of letters from a to z
```bash
echo {a..z}
```
