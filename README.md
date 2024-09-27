Learning AWS - Federation Abuse from Cloud Hacktricks : https://cloud.hacktricks.xyz/pentesting-cloud/aws-security/aws-basic-information/aws-federation-abuse#oidc-github-actions-abuse

While exploring AWS, I delved into federation abuse techniques, specifically leveraging GitHub Actions for privilege escalation. Here's a breakdown of what I learned.

I started by enumerating the lab’s IAM policy using the following command:
aws iam get-policy-version --policy-arn <policy-arn> --version-id <version-id> --profile profilename

This command retrieves the details of a specific IAM policy version. From there, I uncovered the following policy structure:

<img width="724" alt="image" src="https://github.com/user-attachments/assets/f72267cd-9940-4982-b602-f9fa5d09068c">

This policy specifies a condition that targets repositories with names matching a certain pattern (repo:*hacktricks-training*). This allows GitHub Actions to assume the role.

Key Insight
By observing the wildcard in the repository name (*reponame), I realized that I could exploit this condition. I created my this GitHub repository using the same naming convention and leveraged GitHub Actions to gain a valid user session.

With this, I was able to assume the role and access the secrets stored in AWS, ultimately revealing the flag.

Conclusion
This exercise gave me valuable insight into how misconfigured IAM policies can lead to privilege escalation. The lesson here is the importance of carefully defining conditions in federated access policies to avoid unintended access.

