# End-to-End Guide — Java Web App on AWS EC2 (with VS Code Remote - SSH)

This guide mirrors the exact workflow I used to set up a simple Java web application on a cloud VM and edit it remotely.

---

## 1) Launch the EC2 instance

1. Go to **AWS Console → EC2 → Launch instance**.
2. Choose an AMI (e.g., **Amazon Linux 2023** or **Ubuntu 22.04**).
3. Instance type: **t2.micro** (fits Free Tier).
4. **Create a key pair** (PEM) and download it (e.g., `nextwork-keypair.pem`).
5. **Security group**:
   - Inbound: **SSH (22)** from **My IP** only.
6. Launch and note the **Public IPv4 DNS** (e.g., `ec2-xx-xx-xx-xx.compute-1.amazonaws.com`).

Why: The instance hosts the web app files; SSH access lets you manage it remotely.

---

## 2) Secure your PEM locally

- **Windows (PowerShell/Command Prompt):**

  ```bat
  icacls C:\path\to\nextwork-keypair.pem /inheritance:r
  icacls C:\path\to\nextwork-keypair.pem /grant:r %USERNAME%:R
  ```

- **macOS/Linux:**

  ```bash
  chmod 400 ~/path/to/nextwork-keypair.pem
  ```

Reason: SSH refuses to use private keys with overly-permissive file permissions.

---

## 3) SSH into the instance

From your local terminal:

```bash
ssh -i /path/to/nextwork-keypair.pem ec2-user@<EC2-PUBLIC-DNS>   # Amazon Linux
# or
ssh -i /path/to/nextwork-keypair.pem ubuntu@<EC2-PUBLIC-DNS>     # Ubuntu
```

If it’s your first time, accept the host key fingerprint.

---

## 4) Install Java & Maven on the instance

Below are common examples; use the variant matching your AMI.

- **Amazon Linux 2023:**

  ```bash
  sudo dnf update -y
  sudo dnf install -y java-17-amazon-corretto maven git
  java -version
  mvn -version
  ```

- **Ubuntu 22.04:**

  ```bash
  sudo apt update
  sudo apt install -y openjdk-17-jdk maven git
  java -version
  mvn -version
  ```

---

## 5) Generate a Java web app (Maven)

You can run Maven interactively:

```bash
mvn archetype:generate
```

Or non-interactively (example values):

```bash
mvn archetype:generate   -DgroupId=com.example   -DartifactId=cloud-webapp   -DarchetypeArtifactId=maven-archetype-webapp   -DinteractiveMode=false
```

This creates a minimal **Java WebApp** layout:

```
cloud-webapp/
├── pom.xml
└── src/
    └── main/
        └── webapp/
            └── index.jsp
```

---

## 6) Connect with VS Code (Remote - SSH)

1. Install **VS Code** and the **Remote - SSH** extension.
2. In VS Code, press **F1 → Remote-SSH: Add New SSH Host...**.
3. Enter the SSH command (for example):

   ```
   ssh -i /path/to/nextwork-keypair.pem ec2-user@<EC2-PUBLIC-DNS>
   ```

4. Save to your SSH config. Then **Remote-SSH: Connect to Host...** and pick it.
5. Open the generated project folder on the instance and locate:

   ```
   src/main/webapp/index.jsp
   ```

6. Edit `index.jsp` and save. The changes are on the server immediately.

---

## 7) Build (optional)

From the project root on the instance:

```bash
mvn validate
mvn compile
mvn package   # produces a WAR for deployment to a servlet container
```

> Note: The Maven webapp archetype creates a standard WAR project. To serve it, deploy the WAR to a servlet container (e.g., Tomcat/Jetty) or add an embedded server. This repo focuses on scaffolding + remote editing.

---

## 8) GitHub setup

1. Initialize Git and commit:

   ```bash
   git init
   git add .
   git commit -m "Initial commit: Maven webapp + docs"
   ```

2. Create a new GitHub repo, then add the remote and push:

   ```bash
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo>.git
   git push -u origin main
   ```

---

## Troubleshooting

- **Permission denied (publickey):** Ensure the `.pem` file permissions are restricted and the correct user (`ec2-user` vs `ubuntu`) is used.
- **Can’t connect to SSH:** Verify security group allows port 22 from your current IP. Re-check the instance’s public DNS.
- **Maven not found:** Install Maven via your OS package manager.
- **Slow edits via Remote-SSH:** Consider enabling VS Code file watchers/telemetry selectively and closing large folders.

---

## Security considerations

- Restrict SSH to your IP and disable password auth (key-only).
- Rotate or replace the key pair if it’s ever exposed.
- Use IAM roles (instead of long-lived creds) for apps you deploy on the instance.
- Keep the OS and packages updated.

---

## Appendix — Quick commands

```bash
# Example SSH
ssh -i ~/keys/nextwork-keypair.pem ec2-user@ec2-203-0-113-25.compute-1.amazonaws.com

# Example file layout after Maven archetype
tree -L 3

# Build lifecycle
mvn clean package
```