
# Information

Plan Storage | Minutes | (per month)
-------------|---------|-------------
GitHub Free  | 500 MB  | 2,000
GitHub Pro   | 1 GB    | 3,000

Standard GitHub-hosted runners for public repositories

- Linux: 4CPU 16GB-RAM 14GB-SSD x64 (ubuntu-latest, ubuntu-24.04, ubuntu-22.04)
- Linux: 4CPU 16GB-RAM 14GB-SSD arm64 (ubuntu-24.04-arm, ubuntu-22.04-arm)

Standard GitHub-hosted runners for private repositories

- Linux: 2CPU 7GB-RAM 14GB-SSD x64 (ubuntu-latest, ubuntu-24.04, ubuntu-22.04)

## Actions

- [actions/checkout@v5](https://github.com/actions/checkout)
- [actions/setup-python@v5](https://github.com/actions/setup-python)
- [ad-m/github-push-action@v1.0.0](https://github.com/ad-m/github-push-action)

## Example 1 

1. Create a .github/workflows directory in your repository on GitHub if this directory does not already exist.

2. In the .github/workflows directory, create a file named github-actions.yml. For more information, see ["Creating new files."](https://docs.github.com/en/github/managing-files-in-a-repository/creating-new-files)

3. Copy the following YAML contents into the github-actions.yml file

```yml
name: GitHub Actions 
on: [push]
jobs: 
    Explore-GitHub-Actions:
        runs-on: ubuntu-latest
        steps:
            - run: echo "The job was automatically triggered by a ${{ github.event_name }} event."
            - name: Check out repository code
              uses: actions/checkout@v5
            - run: echo "The ${{ github.repository }} repository has been cloned to the runner."
            - name: List files in the repository
              run: | 
                ls ${{ github.workspace }}
            - run: echo "This job's status is ${{ job.status }}."
```

4. Committing the workflow file to a branch in your repository triggers the push event and runs your workflow.

5. Go to the Actions tab to see the workflow information


## Example 2 (Python + CronJob)

```python
# requirements.txt

```

```python
# my_script.py
import logging
import logging.handlers

print("Hello World")

logger = logging.getLogger(__name__)
logger.setLevel(logging.DEBUG)
logger_file_handler = logging.handlers.RotatingFileHandler(
    "status.log",
    maxBytes=1024 * 1024,
    backupCount=1,
    encoding="utf8",
)

logger_file_handler.setFormatter(logging.Formatter("%(asctime)s - %(name)s - %(levelname)s - %(message)s"))
logger.addHandler(logger_file_handler)

logger.info(f'hello world')
```

- Enable ['allow Github Actions to create and approve pull requests'](https://github.com/ad-m/github-push-action?tab=readme-ov-file#requirements-and-prerequisites)
- Enable ['read and write permissions'](https://github.com/ad-m/github-push-action?tab=readme-ov-file#requirements-and-prerequisites)

```yml
name: GitHub Actions 

on:
  push:
    branches:
      - 'main'
  schedule:
    - cron: '0 0 * * *' # Daily at midnight UTC

jobs: 
    running_python_script_with_logging:
        runs-on: ubuntu-latest
        steps:
            - run: echo "The job was automatically triggered by a ${{ github.event_name }} event."

            - name: Checkout repository
              uses: actions/checkout@v5

            - name: Set up Python
              uses: actions/setup-python@v5
              with:
                python-version: '3.12'

            - name: Install dependencies
              run: pip install -r requirements.txt 

            - name: Run Python script
              env:
                MY_SECRET: ${{ secrets.MY_SECRET }}
              run: python my_script.py # Execute your Python script
            
            - run: echo "This job's status is ${{ job.status }}."

            - name: commit files
              run: |
                git config --local user.email "action@github.com"
                git config --local user.name "GitHub Action"
                git add -A
                git diff-index --quiet HEAD || (git commit -a -m "updated logs" --allow-empty)
                
            - name: push changes
              uses: ad-m/github-push-action@v1.0.0
              with:
                github_token: ${{ secrets.GITHUB_TOKEN }}
                branch: main 
```
-- 

References: 

- [GitHub Actions billing](https://docs.github.com/en/billing/concepts/product-billing/github-actions)
- [Quickstart for GitHub Actions](https://docs.github.com/en/actions/get-started/quickstart)
- [Trigger workflow#schedule](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows#schedule)
- [Let’s run cron jobs using Github Actions](https://medium.com/nerd-for-tech/lets-run-cron-jobs-using-github-actions-df64496ffc4a)
- [Run your GitHub Actions workflow on a schedule](https://jasonet.co/posts/scheduled-actions)
- [How to schedule Python scripts with GitHub Actions](https://www.python-engineer.com/posts/run-python-github-actions/)