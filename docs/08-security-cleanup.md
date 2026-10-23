# 8. Security and cost cleanup

## Security checklist
- [ ] Restrict SSH port 22 to your current IP.
- [ ] Restrict Jenkins port 8080 to your IP or private network.
- [ ] Do not expose Jenkins over plain HTTP publicly.
- [ ] Never commit `.pem` files, AWS credentials, GitHub tokens, webhook secrets, or passwords.
- [ ] Keep Jenkins and OS packages updated.
- [ ] Understand that Docker group membership grants powerful host-level access.
- [ ] Use least-privilege IAM permissions if extending the project.
- [ ] Use versioned image tags and a rollback strategy in production.

## Cleanup
1. Save source, docs, and screenshots to GitHub.
2. Remove the demo container if no longer needed:
   ```bash
   docker rm -f cicd-test
   ```
3. Decide whether to stop or terminate EC2. **Termination is destructive.** Verify that you no longer need the instance or its data.
4. Check EBS volumes, snapshots, Elastic IPs, load balancers, NAT gateways, and other billable resources.
5. Review AWS Billing and Cost Management.
6. Stopping EC2 does not stop every possible charge; storage and other resources can still cost money.
