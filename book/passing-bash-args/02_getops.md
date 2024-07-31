# Passing in Arguments using getopts

So far we have passed in basic arguments, however, what if we wanted to pass in more complex arguments? This is where the `getopts` command comes in. The `getopts` command is a built-in command in bash that is used to parse command line arguments. It is used to parse short options (single character options) and their arguments. 

Let us start by defining a simple flag using `getopts`. We will define flags `-v` and `-c` that will print the version of the script, or display a copyright statement. We can define the flags with the following code:

```bash
#!/bin/bash

# Parse the command line arguments
while getopts ":vc" opt; do
  case $opt in
    v)
      echo "Version 1.0"
      exit 0
      ;;
    c)
      echo "Copyright 2024"
      exit 0
      ;;
    ?)
      echo "Invalid option: -$OPTARG"
      exit 1
      ;;
  esac
done
```

What is happening here is that we are using the `getopts` command to parse the command line arguments. The `getopts` command takes three arguments: the options string, the name of the variable to store the parsed option, and the name of the variable to store the parsed argument. In this case, we are using the options string `:vc`, which means that the script accepts two options: `-v` and `-c`. The colon `:` in front of the options string means that the options `-v` and `-c` require an argument.

If we perform the following command:

```shell
sh ./script.sh -v
```

The script will output:

```shell
Version 1.0
```

If we perform the following command:

```shell
sh ./script.sh -c
```

The script will output:

```shell
Copyright 2024
```

If we perform the following command:

```shell
sh ./script.sh -x
```

The script will output:

```shell
Invalid option: -x
```

Now we can utilise basic inputs and flags. But what about multiline inputs? This is where here documents come in.