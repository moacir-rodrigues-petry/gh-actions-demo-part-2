# Prompts

1 - Generate a simple github actions demo

`generate a simple github actions demo like listing the files in the current directory`

Also request to count the lines in the README.md file, the result sees like this:

```yaml
name: List files in directory
on:
  push:
    branches:
      - main

jobs:
  list_files:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: List files
        run: |
          echo "Listing files in the current directory:"
          ls -al
          echo "Counting lines in README.md:"
          wc -l README.md
```

2 -
