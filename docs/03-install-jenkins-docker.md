# 3. Install Docker and Jenkins

> Package repositories and supported Java versions change. Check the current official Docker and Jenkins installation guides before setting up a new host.

## Update Ubuntu
```bash
sudo apt update
sudo apt upgrade -y
```

## Install Docker
```bash
sudo apt install -y docker.io
sudo systemctl enable --now docker
sudo systemctl status docker --no-pager
docker --version
```

The Jenkins service account needs Docker access. The learning lab used:

```bash
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
```

**Security warning:** Docker group membership effectively grants root-level control of the host. Use this only on a controlled lab instance.

## Install Jenkins
Install a supported Java runtime, then add the official Jenkins package repository and install Jenkins following the current official Jenkins Linux guide.

```bash
sudo systemctl enable --now jenkins
sudo systemctl status jenkins --no-pager
```

Complete the initial browser setup using the administrator password path given by the Jenkins installation guide (commonly `/var/lib/jenkins/secrets/initialAdminPassword`).

## Verify
```bash
sudo systemctl is-active docker
sudo systemctl is-active jenkins
```

Open `http://YOUR_EC2_PUBLIC_IP:8080` only if Jenkins is running and access is restricted.

## Memory issue encountered
The small EC2 host experienced an OOM kill. A 2 GiB swap file was added temporarily:

```bash
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
free -h
```

To enable after reboot, add this line to `/etc/fstab` only if absent:

```text
/swapfile none swap sw 0 0
```

Use `sudo nano /etc/fstab`; do not type the line as a shell command. Verify with `swapon --show`. Swap is not a substitute for sufficient RAM.
