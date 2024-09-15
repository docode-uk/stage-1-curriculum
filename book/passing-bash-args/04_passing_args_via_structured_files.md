# Passing Arguments via Structured Files

Structured files are very powerful. We can easily read them, edit specific fields, and serialize the data in them to be passed over a network, to other scripts, or easily written in a database. The most straightforward well known structured file for parameters is a JSON file. Before we dive into JSON files, we need to install `jq` to parse JSON files with the following command:

### MacOS
```shell
brew install jq
```

### Linux
```shell
sudo apt-get install jq
```

### Windows
```shell
choco install jq
```

Now that we have `jq` installed, let us create a JSON file called `input.json` with the following content:

```json
{
  "name": "John Doe",
  "age": 30,
  "email": "john.doe@example.com"
}
```

We can read the JSON file with the following script:

```bash
#!/bin/bash

# Ensure the script receives the JSON file as an argument
if [ "$#" -ne 1 ]; then
  echo "Usage: $0 <json-file>"
  exit 1
fi

# Read the JSON file
json_file="$1"

# Extract fields using jq
name=$(jq -r '.name' "$json_file")
age=$(jq -r '.age' "$json_file")
email=$(jq -r '.email' "$json_file")

# Use the extracted fields in the script
echo "Name: $name"
echo "Age: $age"
echo "Email: $email"
```

Here we can see that `jq` has a fairly high level abstraction. We are pointing to the JSON file, read it, and extract the `name` field with the following code:

```bash
name=$(jq -r '.name' "$json_file")
```

We can run our script with the following command:

```shell
sh ./script.sh input.json
```

The script will produce the following output:

```shell
Name: John Doe
Age: 30
Email: john.doe@example.com
```

And this is it, we can also do the exact same approach with `yaml` files using `yq` package.

Writing to a `JSON` file is a little fiddly but not impossible. Below is a script on how to alter/update some fields in an existing `JSON` file:

```bash
#!/bin/bash

FILE_PATH="./store.json"

# Create a temporary file
tmp_file=$(mktemp)

# Use jq to modify the JSON and write to the temporary file
jq '.age = 31 | .phone = "123-456-7890" | .address = "123 Main St"' "$FILE_PATH" > "$tmp_file"

# Check if jq command succeeded
if [ $? -eq 0 ]; then
  # Move the temporary file to overwrite the original file
  mv "$tmp_file" "$FILE_PATH"
  echo "Modified JSON written to $FILE_PATH"
else
  echo "An error occurred while modifying the JSON."
  rm "$tmp_file"
fi
```

We can see that we must create a temporary file to write the new JSON file to. We then then move the temporary file to the original file. It must be noted that the `store.json` file must exist before running and have the correct formating for `jq` to work correctly. If you want the file to be empty, the file must have `{}` in it. 

Args can also be passed into the `jq` command with the following code:

```bash
jq --arg field "$field_name" --arg value "$field_value" '.[$field] = $value' "$FILE_PATH" > "$tmp_file"
```

To delete a field we must use the `del` command with the following code:

```bash
jq --arg field "$field_name" 'del(.[$field])' "$FILE_PATH" > "$tmp_file"
```