# 9. Interview explanation and questions

## 60-second explanation
“I built an automated CI/CD pipeline for a Dockerized web application. The source is stored in GitHub. When I push a change, a GitHub webhook triggers Jenkins. Jenkins checks out the code, builds a Docker image using the Dockerfile, removes the old application container, and starts a new Nginx container on AWS EC2. I tested this by changing the web page and confirmed that Jenkins succeeded and the updated content appeared in the browser.”

## Explain the technologies
- **GitHub:** stores source code.
- **Webhook:** notifies Jenkins about a push.
- **Jenkins:** automates pipeline stages.
- **Dockerfile:** instructions for building the image.
- **Image:** packaged application template.
- **Container:** running instance of the image.
- **EC2:** cloud virtual machine.
- **Nginx:** serves the HTML page.

## Common questions

**What triggers the pipeline?**  
A GitHub push event reaches the webhook endpoint and the configured Jenkins job starts.

**What are the stages?**  
Checkout, Build Docker Image, and Deploy Application.

**Why Docker?**  
It packages the application and runtime environment for consistent execution.

**What does `-p 8081:80` mean?**  
Host port 8081 forwards traffic to port 80 inside the container.

**Why use `docker rm -f cicd-test || true`?**  
It removes the old container if present; `|| true` prevents a missing container from failing the shell step. Production deployment needs more careful error handling.

**What issue did you solve?**  
The EC2 host ran low on memory and experienced an OOM kill. I added swap as a temporary mitigation and verified it was active. Swap is not a replacement for enough RAM.

**Is this production-ready?**  
No. It is a learning lab. Production needs stronger access controls, HTTPS, secrets management, health checks, rollback, monitoring, and a more isolated architecture.

## Demo checklist
1. Show the repository and explain each file.
2. Explain each Jenkinsfile stage.
3. Show a webhook delivery.
4. Show successful Jenkins Console Output.
5. Show the website with the latest change.
6. Explain one troubleshooting issue.
