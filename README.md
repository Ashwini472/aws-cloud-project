 🚀 Automated AWS EC2 Web Server with S3 Backup & CloudWatch Monitoring

 📌 Project Overview
This project demonstrates how to deploy a secure, highly available Apache web server on **Amazon EC2**, automate off-site website backups to **Amazon S3** using custom **Bash shell scripting** and **Cron jobs**, and monitor infrastructure performance with **Amazon CloudWatch**.

The infrastructure uses **AWS IAM Roles** for secure inter-service authentication, eliminating the need to store hardcoded access keys on the server.

---

 🏗️ Architecture Diagram

```text
                  🌐 Internet User
                         │
                         ▼ (HTTP Port 80 / SSH Port 22)
                ┌─────────────────┐
                │ Security Group  │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │   Amazon EC2    │ ──(Monitored by CloudWatch)
                │  (Amazon Linux) │
                │  Apache Server  │
                └────────┬────────┘
                         │
               IAM Role (Temporary Keys)
                         │
                         ▼
                ┌─────────────────┐
                │    Amazon S3    │
                │  Backup Bucket  │
                └─────────────────┘
```

---

## 🛠️ Key Technical Features

1. Web Hosting**: Deployed Apache (`httpd`) on Amazon Linux 2023 to serve an interactive web dashboard.
2. Keyless AWS Authentication**: Attached an IAM Role (`EC2-S3-Backup-Role`) to the EC2 instance to grant temporary, secure permissions for S3 operations.
3. Automated Backup Pipeline**: Developed a shell script (`/opt/scripts/s3_backup.sh`) that:
   - Compresses `/var/www/html` into a timestamped `.tar.gz` archive.
   - Uploads the archive to an S3 bucket (`backups/` prefix).
   - Automatically cleans up local temporary files from `/tmp`.
4. Task Scheduling**: Configured `cronie` (`0 2 * * *`) to execute the backup script automatically every night at 2:00 AM.
5. System Observability**: Tracked CPU utilization and network I/O spikes in Amazon CloudWatch.

---

## 📁 Repository Structure

- [`index.html`](./index.html): Interactive website frontend with dynamic clock and backup simulator.
- [`scripts/s3_backup.sh`](./scripts/s3_backup.sh): Production Bash automation script for S3 synchronization.

---

## 📷 Screenshots & Proof of Work

### 1. Live Web Server
![Live Web Server](./images/live-website.png)

### 2. S3 Backup Storage Verification
![S3 Backups](./images/s3-backups.png)

### 3. CloudWatch Monitoring
![CloudWatch Metrics](./images/cloudwatch-metrics.png)
