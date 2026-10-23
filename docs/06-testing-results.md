# 6. Testing and results

## Confirmed in the original lab
- GitHub push triggered Jenkins automatically.
- Jenkins checked out commit `919fb5da8a2083c5db2aec9b5cbfa8f9ce9ebe15`.
- `cicd-webapp:latest` built successfully.
- The old `cicd-test` container was removed and a new one started.
- Jenkins ended with `Finished: SUCCESS`.
- The web page showed `Automatic deployment test`.

## Verify on EC2
```bash
sudo systemctl status jenkins --no-pager
sudo systemctl status docker --no-pager
docker image ls
docker ps
docker logs --tail 50 cicd-test
curl -I http://localhost:8081
```

Expect active services, the image and container to be present, and an HTTP success response such as `200 OK`.

## Repeat the test
Edit `index.html`, commit to `main`, wait for Jenkins, confirm success, then refresh the site.

Add genuine screenshots using the filenames in `../screenshots/README.md`. Blur account IDs, tokens, and any private information.
