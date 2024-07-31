# Here Documents

If we want to pass a large amount of data to a command, we can use a here document. A here document is a way to pass a block of text to a command. Here is an example of a here document:

```bash
cat << EOF
This is a here document.
It can span multiple lines.
EOF
```

Here the `cat` command reads the text between `<< EOF` and `EOF` and prints it to the standard output. The text between `<< EOF` and `EOF` is called the here document. The `EOF` is called the delimiter. The delimiter can be any word, but it is common to use `EOF` which stands for "end of file".

Lets create a simple script and pass in a here document. First we create a script called `script.sh` that just prints the first argument passed to it with the following code:

```bash
#!/bin/bash

echo $1
```

Now we can pass a here document to the script with the following command:

```shell
sh ./script.sh "$(cat <<EOF
This is line 1
This is line 2
This is line 3
EOF
)"
```

Here we are assigning the printout of the here document into one string by wrapping the printout in `$(...)`. The script will output:

```shell
This is line 1 This is line 2 This is line 3
```
This is all one line because the string has concatenated the lines together and passed the entire string as the first argument to the script. We can read the entire input including the new lines of a here document by using a while loop. Here is an example of a script that reads a here document line by line with the code below:

```bash
#!/bin/bash

while IFS= read -r line; do
    echo "$line"
done
```

We can break down what is going on in this script with the following bullet points:

- **while:** This starts a while loop, which will continue to execute as long as the condition (in this case, reading lines from standard input) is true.

- **IFS=:** This sets the Internal Field Separator (IFS) to an empty value temporarily within the loop. The IFS is used by Bash to determine how to split words. By setting it to an empty value, we ensure that leading and trailing whitespace is not trimmed, and that the entire line is read.

- **read -r line:** The read command reads a line from standard input and assigns it to the variable line. -r option tells read to treat backslashes literally (i.e., not as escape characters).

- **; do:** This indicates the start of the loop body. Commands following do will be executed for each line read.

To pass a here document to the script, we can use the following command:

```shell
sh ./script.sh << EOF
This is line 1
This is line 2
This is line 3
EOF
```

The script will output:

```shell
This is line 1
This is line 2
This is line 3
```
Here we can see that our new line characters are preserved and the script reads the input line by line.

We can also pass in data from a file to a script using a here document. First, let us put the following text into a file called `input.txt`:

```shell
This is line 1
This is line 2
This is line 3

```
It is important that we have a new line at the bottom of the `input.txt` otherwise we will cut the input off at the last line and only pass in the first two lines. Now we can pass the contents of `input.txt` to the script with the following command:

```shell
sh ./script.sh < input.txt
```

This will also give the following output:

```shell
This is line 1
This is line 2
This is line 3
```

We have now covered basic arguments, flags, and documents, but what if we want to pass in complex data structures. This is where passing data using structured files comes in. 