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

3 - Generate a job dependency

`generate a job 2 that depends on job 1`

With that we should be good, but let's increment, ask Copilot to print the date and time to validated that job 2 will run just after the job 1, something like this:

`add a date and time print to validate that job2 ran after job1`

The result should be like this:

```yaml
name: Job Dependency Example
on:
  push:
    branches:
      - main

jobs:
  job1:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: Print date and time for job1
        run: |
          echo "Job1 started at:"
          date
      - name: List smallest file
        run: |
          echo "Finding the smallest file in the repository:"
          find . -type f -exec du -b {} + | sort -n | head -n 1

  job2:
    runs-on: ubuntu-latest
    needs: job1
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: Print date and time for job2
        run: |
          echo "Job2 started at:"
          date
      - name: List largest file
        run: |
          echo "Finding the largest file in the repository:"
          find . -type f -exec du -b {} + | sort -n | tail -n 1
```

4 - Generate an artifact to share the result between jobs

`generate a file called my-artifact.txt and put any info in it, create a job name 'Share-Data-With-Another-Job' to upload the artifact, create another job name 'Receiving-Data-From-Another-Job' to download the artifact, and list the content inside of it`

This should be something like this:

```yaml
name: Artifact Example
on:
  push:
    branches:
      - main

jobs:
  Share-Data-With-Another-Job:
    runs-on: ubuntu-latest
    steps:
      - name: Create my-artifact.txt
        run: |
          echo "This is the content of my-artifact.txt file." > my-artifact.txt
      - name: Upload artifact
        uses: actions/upload-artifact@v3
        with:
          name: my-artifact
          path: my-artifact.txt
          retention-days: 7

  Receiving-Data-From-Another-Job:
    runs-on: ubuntu-latest
    needs: Share-Data-With-Another-Job
    steps:
      - name: Download artifact
        uses: actions/download-artifact@v3
        with:
          name: my-artifact
      - name: List content of my-artifact.txt
        run: |
          echo "Content of my-artifact.txt:"
          cat my-artifact.txt
```

5 - Generate a job that runs on a specific schedule
