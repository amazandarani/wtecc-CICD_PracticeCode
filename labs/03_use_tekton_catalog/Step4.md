Step 4: Run the Pipeline

You can now use the Tekton CLI (tkn) to create a PipelineRun to run the pipeline.

Use the following command to run the pipeline, passing in the URL of the repository, the branch to clone, the workspace name, and the persistent volume claim name.

bash

tkn pipeline start cd-pipeline \
    -p repo-url="https://github.com/ibm-developer-skills-network/wtecc-CICD_PracticeCode.git" \
	-p branch="main" \
    -w name=pipeline-workspace,claimName=pipelinerun-pvc \
    --showlog
Run
You should see output similar to this:

text

$ tkn pipeline start cd-pipeline \
>     -p repo-url="https://github.com/ibm-developer-skills-network/wtecc-CICD_PracticeCode.git" \
>     -p branch="main" \
>     -w name=pipeline-workspace,claimName=pipelinerun-pvc \
>     --showlog
PipelineRun started: cd-pipeline-run-mndgw
Waiting for logs to be available...
Eventually, you should see the output from the logs.

Note: There will be multiple lines of output from [clone: clone]. These are not represented below for clarity.

text

[clone : clone] <- There will be many lines from git-clone
[clone : clone] ...
[lint : echo-message] Calling Flake8 linter...
[tests : echo-message] Running unit tests with PyUnit...
[build : echo-message] Building image for https://github.com/ibm-developer-skills-network/wtecc-CICD_PracticeCode.git ...
[deploy : echo-message] Deploying main branch of https://github.com/ibm-developer-skills-network/wtecc-CICD_PracticeCode.git ...
You can always see the pipeline run status by listing the PipelineRuns with:

bash

tkn pipelinerun ls
Run
You should see:

plaintext

NAME                    STARTED          DURATION     STATUS
cd-pipeline-run-mrg6g   45 seconds ago   18 seconds   Succeeded
You can check the logs of the last run with:

bash

tkn pipelinerun logs --last
Run
