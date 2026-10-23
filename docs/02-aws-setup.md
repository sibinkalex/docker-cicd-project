# 2. AWS EC2 setup

## Prerequisites
- AWS account with EC2 permissions.
- GitHub account.
- A local SSH private key (`.pem`). Never upload it to GitHub.

## Historical lab details
The original lab used public IP `18.60.56.84`, private IP `10.0.0.12`, Jenkins at `http://18.60.56.84:8080`, and the app at `http://18.60.56.84:8081`. These are historical values and may no longer work. Use your current instance address if it still exists.

## Setup
1. Open AWS Console → EC2 → Instances.
2. Launch or select an Ubuntu instance.
3. Choose a key pair and store the `.pem` file securely.
4. Note the current public IP.
5. Review its security group.

## Inbound rules

| Port | Purpose | Recommended source |
|---|---|---|
| 22/TCP | SSH | Your current IP only |
| 8080/TCP | Jenkins | Your IP/private network only |
| 8081/TCP | Website | Your IP, unless public demo access is needed |

Do not leave SSH or Jenkins open to `0.0.0.0/0`.

## Connect from Windows PowerShell
Run on your **Windows computer**, in the folder containing your key:

```powershell
ssh -i "mumbai.pem" ubuntu@YOUR_EC2_PUBLIC_IP
```

Replace the placeholder. Do not run this from inside EC2; the key should remain on your computer.
