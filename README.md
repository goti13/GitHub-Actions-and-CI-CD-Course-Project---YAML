# GitHub-Actions-and-CI-CD-Course-Project---YAML

Understanding YAML syntax for workflows.

Lesson 1: Workflow and syntax structure

Objectives:

1. ﻿﻿﻿Understand YAML syntax for workflows.
2. ﻿﻿﻿Learn the structure and components of a workflow.

Lesson Details:

1. YAML Syntax for Workflows:
   
- YAML is a human-readable data serialization standard used for configuration files.
- ﻿﻿Key concepts: indentation, key-value pairs, lists.
- Example snippet:

```
name: Example Workflow
on: [push]

```

2. Workflow Structure and Components:

- Workflow File: Located in '•github/workflows' directory, e.g., 'main.yml'.
- ﻿﻿Jobs: Define tasks like building, testing, deploying.
- ﻿﻿Steps: Individual tasks within a job.
- Actions: Reusable units of code within steps.
- ﻿﻿Events: Triggers for the workflow, e.g., 'push', 'pull_request'.
- ﻿﻿Runners: The server where the job runs, e.g., 'ubuntu-latest'.


Implementing Continuous Integration

Lesson 2: Building and Testing Code

Objectives:

1. Set up build steps in GitHub Actions.
2. Run tests as part of the Cl process.

   
Setting Up Build Steps:

1. Defining the Build Job:
   
- ﻿﻿In your GitHub Actions workflow file (e.g.,' github/workflows/main.yml*), start by defining a job named 'build'.
- This job is responsible for building your code:

  ```
  jobs:
    build:
      runs-on: ubuntu-latest
      steps:
      # Steps will be defined next
  
  ```

2. Adding Build Steps:
- Each step in the job performs a specific task.
- Here, we add three steps: checking out the code, installing dependencies, and running the build script.

```
steps:
- uses: actions/checkout@v2
  # 'actions/checkout@v2' is a pre-made action that checks out your repository under $GITHUB_WORKSPACE, so your workflow can access it.

- name: Install dependencies
  run: npm install
  # 'npm install' installs the dependencies defined in your project's 'package.json' file.

- name: Build
  run: npm run build
  # 'npm run build' runs the build script defined in your 'package.json'. This is typically used for compiling or preparing your code for deployment.

```

Running Tests in the Workflow:

1. Adding Test Steps:
   
- After the build steps, include steps to execute your test scripts.
- ﻿﻿This ensures that your code is not only built but also passes all the tests.

```
- name: Run tests
  run: npm test
  # 'npm test' runs the test script defined in your 'package.json'. It's crucial for ensuring that your code works as expected before deployment.

```
Important Notes:

- The 'build' job consists of steps to check out the code, install dependencies, build the code, and run tests.
- ﻿﻿The ' runs-on: ubuntu-latest' line specifies that the job should run on the latest version of Ubuntu provided by GitHub Actions.
- ﻿﻿Using actions like 'actions/checkout@v2* helps in leveraging community-maintained actions to simplify common tasks.
- ﻿﻿Commands like 'npm install', 'npm run build', and 'npm test' are standard Node.js commands used for managing dependencies, building, and testing Node.js applications.


Additional YAML Concepts in GitHub Actions

Objectives:
- Deepen understanding of advanced YAML features used in GitHub Actions.
- ﻿﻿Explore the use of environment variables and secrets in workflows.

Detailed Steps and Code Explanation:


1. Using Environment Variables:
   
- ﻿﻿Environment variables can be defined at the workflow, job, or step level.
- ﻿﻿They allow you to dynamically pass configuration and settings.

```
env:
  CUSTOM_VAR: value
  # Define an environment variable 'CUSTOM_VAR' at the workflow level.

jobs:
  example:
    runs-on: ubuntu-latest
    steps:
    - name: Use environment variable
      run: echo $CUSTOM_VAR
      # Access 'CUSTOM_VAR' in a step.
```

2. Working with Secrets:
   
- Secrets are encrypted variables set in your GitHub repository settings.
- ﻿﻿Ideal for storing sensitive data like access tokens, passwords, etc.

```
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Use secret
      run: |
        echo "Access Token: ${{" secrets.ACCESS_TOKEN "}}"
        # Use 'ACCESS_TOKEN' secret defined in the repository settings.
```

3. Conditional Execution:
   
- You can control when jobs, steps, or workflows run based on conditions

```
jobs:
  conditional-job:
    runs-on: ubuntu-latest
    if: github.event_name == 'push' && github.ref == 'refs/heads/main'
    # The job runs only for push events to the 'main' branch.
    steps:
    - uses: actions/checkout@v2
```

4. Using Outputs and Inputs between Steps:
   
- Share data between steps in a job using outputs.

```
jobs:
  example:
    runs-on: ubuntu-latest
    steps:
    - id: step-one
      run: echo "::set-output name=value::$(echo hello)"
      # Set an output named 'value' in 'step-one'.
    - id: step-two
      run: |
        echo "Received value from previous step: ${{" steps.step-one.outputs.value "}}"
        # Access the output of 'step-one' in 'step-two'.
```

Important Notes:
- Environment variables and secrets are crucial for managing configurations and sensitive data in your CI/ CD pipelines.
- ﻿﻿Conditional execution helps tailor the workflow based on specific criteria, making your Cl/CD process more efficient.
- ﻿﻿Sharing data between steps using outputs and inputs allows for more complex workflows where the output of one step can influence or provide data to subsequent steps.
- These advanced features enhance the flexibility and security of your GitHub Actions workflows, enabling a more robust CI/CD process.
