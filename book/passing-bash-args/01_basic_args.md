
# Passing Basic Args to a Bash Scripts

As we are automating repetitive tasks with bash scripts, we can notice that our bash scripts can become a little single use. For instance, let us imagine that we want to delete all `.txt` and `.log` files in a directory. We can achieve this writing the following script:

```bash
#!/bin/bash

# Directory containing the log files
LOG_DIR="./logs"

# Check if the directory exists
if [ -d "$LOG_DIR" ]; then
  # Delete all .log and .txt files in the directory
  rm -f "$LOG_DIR"/*.log "$LOG_DIR"/*.txt
  echo "All .log and .txt files in $LOG_DIR have been deleted."
else
  echo "Directory $LOG_DIR does not exist."
fi
```

However, what if we want to delete all `.log` files in a different directory? We would have to change the script. This is not a big deal, but it would be nice if we could pass the directory as an argument to the script. This way, we could reuse the script for different directories.

To pass arguments to a bash script, we can use the `$1`, `$2`, `$3`, etc. variables. These variables represent the first, second, third, etc. arguments passed to the script. For instance, if we run the following script:

```bash
#!/bin/bash

echo "The first argument is $1"
echo "The second argument is $2"
echo "The third argument is $3"
```
It must be noted that we start our arguments at `$1` and not `$0`. This is because `$0` is the name of the script itself.

We can pass arguments to the script with the command below:

```shell
sh ./script.sh one two three
```

This would give the following output:

```shell
The first argument is one
The second argument is two
The third argument is three
```

Now, let us modify the script to delete all `.log` files in a directory passed as an argument with the following code:

```bash
#!/bin/bash

# Directory containing the log files
LOG_DIR="$1"

# Check if the directory exists
if [ -d "$LOG_DIR" ]; then
  # Delete all .log files in the directory
  rm -f "$LOG_DIR"/*.log
  echo "All .log files in $LOG_DIR have been deleted."
else
  echo "Directory $LOG_DIR does not exist."
fi
```

Now, we can run the script with the following command:

```shell
sh ./script.sh ./logs
```

However, if we pass no arguments to the script, the script will fail. To avoid this, we can check if the number of arguments passed to the script is correct. We can do this with the `$#` variable, which contains the number of arguments passed to the script. We can check if the number of arguments is correct with the following code:

```bash
#!/bin/bash

# Check if the number of arguments is correct
if [ "$#" -ne 1 ]; then
  echo "Usage: $0 <directory>"
  exit 1
fi

# Directory containing the log files
LOG_DIR="$1"

# Check if the directory exists
if [ -d "$LOG_DIR" ]; then
  # Delete all .log files in the directory
  rm -f "$LOG_DIR"/*.log
  echo "All .log files in $LOG_DIR have been deleted."
else
  echo "Directory $LOG_DIR does not exist."
fi
```

It must be noted that we exit with a `1` status code meaning that something went wrong. This can inform processes like CI/CD pipelines that the script failed. We can also see that we get the number of arguments passed into the script using `$#`. If we run the script without arguments, we will get the following output:

```shell
Usage: script.sh <directory>
```

Here we are telling the user that they must pass a directory. This is a good practice to make our scripts more user-friendly. We run the script with the correct arguments our command will look like the following:

```shell
sh script.sh ./logs
```

This will then delete all `.log` files in the `./logs` directory. However, what if we wanted to specify any number of file types that we want to delete? This is where recursive commands come in.

## Passing recursive Basic Args to a Bash Scripts

We can pass any number of arguments to a bash script by using the `$@` variable. This variable contains all the arguments passed to the script. We can loop through all the arguments with the following code:

```bash
#!/bin/bash

for VARIABLE in "$@"
do
    echo $VARIABLE
done
```

If we run the script with the following command:

```shell
sh script.sh one two three
```

We will get the following output:

```shell
one
two
three
```

For recursive arguments we may not know the exact number of arguments being passed in, so it is usually best practice to have them at the end of the argument chain. For instance, if we were to have a script that deletes a range of file types in a directory, we would pass the directory into the script first, and then process all of the file type arguments in afterwards. We can do this with the following code:

```bash
#!/bin/bash

# Check if the number of arguments is correct
if [ "$#" -lt 2 ]; then
  echo "Usage: $0 <directory> <file types>"
  exit 1
fi

# Directory containing the log files
LOG_DIR="$1"

# Check if the directory exists
if [ -d "$LOG_DIR" ]; then
  # Loop through all the file types
  for FILE_TYPE in "${@:2}"
  do
    # Delete all files of the file type in the directory
    rm -f "$LOG_DIR"/*.$FILE_TYPE
    echo "All .$FILE_TYPE files in $LOG_DIR have been deleted."
  done
else
  echo "Directory $LOG_DIR does not exist."
fi
```

Here we can see that we initially check that the number or agruments passed into the script are at least `2`. This is because we need at least a directory and one file type to delete. We then loop through all of the file types passed in and delete all files of that type in the directory. We can run the script with the following command:

```shell
sh ./script.sh ./logs txt log onnx
```

This gives the output below:

```shell
All .txt files in ./logs have been deleted.
All .log files in ./logs have been deleted.
All .onnx files in ./logs have been deleted.
```

Here we can see that we have deleted all `.txt`, `.log`, and `.onnx` files in the `./logs` directory. This is a great way to make our scripts more flexible and reusable. We can now use this script to delete any file type in any directory.
