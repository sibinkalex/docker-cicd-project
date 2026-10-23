# 4. GitHub repository and webhook

Repository: https://github.com/sibinkalex/docker-cicd-project

## Commit a change
```bash
git clone https://github.com/sibinkalex/docker-cicd-project.git
cd docker-cicd-project
# Edit index.html
git add index.html
git commit -m "Update website content"
git push origin main
```

You can also edit the file in GitHub's web editor and commit to `main`. Never put tokens or passwords in source files.

## Configure webhook
In repository **Settings → Webhooks → Add webhook**:
1. Payload URL: `http://YOUR_EC2_PUBLIC_IP:8080/github-webhook/` (the original temporary lab used HTTP).
2. Content type: `application/json`.
3. Configure a secret if supported and validated; keep it private.
4. Select **Just the push event**.
5. Enable **Active** and add it.
6. Check Recent Deliveries after a push.

Use HTTPS and secure Jenkins for any real deployment.

## Verified lab event
Commit `919fb5da8a2083c5db2aec9b5cbfa8f9ce9ebe15` added the text `Automatic deployment test`. Jenkins reported `Started by GitHub push by sibinkalex`, and the browser showed the updated page.
