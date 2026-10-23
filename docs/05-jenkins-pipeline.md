# 5. Configure Jenkins pipeline

1. Sign in to Jenkins and ensure Git and Pipeline support are installed.
2. Select **New Item**.
3. Job name: `docker-cicd-pipeline`.
4. Select **Pipeline** and create it.
5. Pipeline Definition: **Pipeline script from SCM**.
6. SCM: **Git**.
7. Repository URL: `https://github.com/sibinkalex/docker-cicd-project.git`.
8. Credentials: none for this public repository.
9. Branch: `*/main`.
10. Script Path: `Jenkinsfile`.
11. Under Build Triggers, select **GitHub hook trigger for GITScm polling**.
12. Save.

## First build
Select **Build Now**, open the build number, and inspect **Console Output**. Expected stages: Checkout, Build Docker Image, Deploy Application. Success ends with `Finished: SUCCESS`.

## Test automatic deployment
1. Change a visible line in `index.html`.
2. Commit and push to `main`.
3. Confirm Jenkins starts without clicking Build Now.
4. Inspect Console Output.
5. Refresh the application URL.

If it does not trigger, check webhook delivery, the current EC2 IP, network rules, and the job trigger setting.
