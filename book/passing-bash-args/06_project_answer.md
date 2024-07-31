
# Project Answer

We can create a basic key value store script with the following:

```bash
#!/bin/bash

FILE_PATH="./store.json"

while getopts ":gpd" opt; do
  case $opt in
    g)
      echo "Getting the value of $2"
      field_name="$2"
      field_value=$(jq -r --arg field "$field_name" '.[$field]' "$FILE_PATH")
      echo "$field_name: $field_value"
      exit 0
      ;;
    p)
      echo "putting the value of $2"
      field_name="$2"
      field_value="$3"
      tmp_file=$(mktemp)
      jq --arg field "$field_name" --arg value "$field_value" '.[$field] = $value' "$FILE_PATH" > "$tmp_file"
      # Check if jq command succeeded
      if [ $? -eq 0 ]; then
        # Move the temporary file to overwrite the original file
        mv "$tmp_file" "$FILE_PATH"
        echo "Modified JSON written to $FILE_PATH"
      else
        echo "An error occurred while modifying the JSON."
        rm "$tmp_file"
      fi
      exit 0
      ;;
    d)
      echo "deleting the value of $2"
      field_name="$2"
      tmp_file=$(mktemp)
      jq --arg field "$field_name" 'del(.[$field])' "$FILE_PATH" > "$tmp_file"
      # Check if jq command succeeded
      if [ $? -eq 0 ]; then
        # Move the temporary file to overwrite the original file
        mv "$tmp_file" "$FILE_PATH"
        echo "Modified JSON written to $FILE_PATH"
      else
        echo "An error occurred while modifying the JSON."
        rm "$tmp_file"
      fi
      exit 0
      ;;
    ?)
      echo "Invalid option: -$OPTARG"
      exit 1
      ;;
  esac
done
```

We have the following commands for the k-v operations:

PUT:
```shell
sh ./kv_store.sh -p surname Doe
```

GET:
```shell
sh ./kv_store.sh -g surname
```

DELETE:
```shell
sh ./kv_store.sh -d surname
```