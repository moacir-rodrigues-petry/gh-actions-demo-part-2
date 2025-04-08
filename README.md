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

2 - Generate 2 jobs

`generate a GitHub Actions job that lists the smallest and largest files in the repository by file size``

This should be the result:

```yaml
name: List files by size
on:
  push:
    branches:
      - main
jobs:
  list_smallest_file:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: List smallest file
        run: |
          echo "Finding the smallest file in the repository:"
          find . -type f -exec du -b {} + | sort -n | head -n 1

  list_largest_file:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: List largest file
        run: |
          echo "Finding the largest file in the repository:"
          find . -type f -exec du -b {} + | sort -n | tail -n 1
```

3 - Generate a job with a matrix
