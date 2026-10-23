# 7. Troubleshooting

## Jenkins unavailable
```bash
sudo systemctl status jenkins --no-pager
sudo journalctl -u jenkins -n 100 --no-pager
```
Check current EC2 IP, security group, and whether Jenkins is running.

## Docker permission denied
On a controlled lab host, this may help:
```bash
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
```
Remember the Docker group is highly privileged.

## Docker build fails
```bash
ls -la
cat Dockerfile
```
Ensure `Dockerfile` and `index.html` are committed to the configured branch.

## Port 8081 is busy
```bash
docker ps
sudo ss -ltnp | grep ':8081'
```
Remove only the lab container if safe:
```bash
docker rm -f cicd-test
```

## GitHub push does not trigger Jenkins
- Inspect GitHub Settings → Webhooks → Recent Deliveries.
- Check the endpoint ends in `/github-webhook/`.
- Verify current EC2 address and network access.
- Confirm the Jenkins trigger is enabled.

## OOM / memory issue
```bash
free -h
swapon --show
sudo journalctl -k --since "2 hours ago" | grep -i -E 'oom|killed process'
```
The lab used 2 GiB swap as a temporary mitigation. Consider a larger instance if memory is still constrained.
