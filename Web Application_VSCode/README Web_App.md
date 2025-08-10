# Set Up a Web App in the Cloud (Java on AWS EC2)

A reproducible walkthrough of how I stood up a simple Java web app on an AWS EC2 instance and edited it remotely from VS Code via the **Remote - SSH** extension.

> This repository captures the exact flow I followed: launch EC2, lock down SSH, connect with a `.pem` key, scaffold a Java web app with Maven, and edit `index.jsp` on the server from VS Code.

## What’s inside

- **Step-by-step guide** in [`docs/SETUP_GUIDE.md`](docs/SETUP_GUIDE.md) (console + VS Code)
- Minimal **Maven WebApp** structure (e.g., `src/main/webapp/index.jsp`)
- Practical SSH and key-handling notes (Windows `icacls` + macOS/Linux `chmod`)

## Prerequisites

- An AWS account with permissions to create EC2 instances and key pairs
- A local machine with:
  - **VS Code** installed (with **Remote - SSH** extension)
  - **OpenSSH client** (Windows 10/11, macOS, or Linux)
- A `.pem` key pair downloaded from AWS
- (On the EC2 host) **Java 17+** and **Maven 3.8+**

## Quick start

1. **Launch EC2** (e.g., Amazon Linux 2023, t2.micro) and **allow SSH from your IP only**.
2. **Download** your key pair (e.g., `nextwork-keypair.pem`) and secure it locally.
3. **SSH into EC2**:

   ```bash
   ssh -i /path/to/nextwork-keypair.pem ec2-user@<EC2-PUBLIC-DNS>
   ```

4. **Install Java & Maven** on the instance (example for Amazon Linux shown in the guide).
5. **Generate the Maven web app** skeleton:

   ```bash
   mvn archetype:generate
   # or non-interactive example:
   mvn archetype:generate -DgroupId=com.example -DartifactId=cloud-webapp -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false
   ```

6. **Use VS Code → Remote - SSH** to open the server and **edit `src/main/webapp/index.jsp`**.
7. Commit and push your work to GitHub.

## Repository structure (example)

```
.
├── docs/
│   └── SETUP_GUIDE.md
├── src/
│   └── main/
│       └── webapp/
│           └── index.jsp
├── pom.xml
└── README.md
```

## Notes & tips

- Keep SSH locked down (source IP only) and rotate keys when needed.
- If you’re on **Windows**, use `icacls` to restrict permissions on the `.pem` file.
- On macOS/Linux, use `chmod 400 path/to/key.pem`.
- If Maven is missing on the instance, install it via the package manager or download from Apache.

## License

MIT (or choose another license for your repo).