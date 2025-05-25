
# ☁️ Amazon Connect Setup Guide

This repository contains a detailed, step-by-step guide for setting up an **IT Help Desk using Amazon Connect**, with integration of **Amazon Lex bots** for intelligent call routing and **chat widgets** for web-based support. This documentation is tailored for Operations Center and IT personnel deploying cloud-based contact center solutions.

---

## 📘 Overview

Amazon Connect is a cloud-based contact center service that enables businesses to deliver customer service at scale. This guide walks you through:

- Creating a new Amazon Connect instance
- Integrating Amazon Lex bots to handle common IT issues like password resets and network problems
- Designing contact flows to route calls and chats intelligently
- Deploying chat widgets for web support
- Testing voice and chat experiences using custom flows

---

## 🧰 Prerequisites

Before starting, make sure you have:

- An **AWS account**
- A **configured Amazon Connect instance**
- **Administrative permissions**
- A **claimed phone number** in Amazon Connect

---

## 🛠️ Setup Steps

### 1. Create and Configure Amazon Connect
- Set up identity management (Amazon Connect users, Directory Service, or SAML 2.0)
- Define admin user and permissions
- Enable telephony and media options (inbound/outbound, early media, multi-party)

### 2. Set Up Data Storage
- Automatically configure Amazon S3 buckets for call recordings, reports, chat transcripts, and email messaging

### 3. Deploy Amazon Lex Bot
- Create a Lex bot named `HelpDesk`
- Add intents like `PasswordReset` and `NetworkIssue` with sample utterances
- Build and test the bot in Amazon Lex console

### 4. Integrate Lex Bot with Amazon Connect
- Add Lex bot to your Amazon Connect instance under the “Flows” section
- Link intents to input blocks in the contact flow

### 5. Create Contact Flow
- Use blocks like `Set Voice`, `Play Prompt`, `Get Customer Input`, `Set Working Queue`, and `Transfer to Queue`
- Route user input based on Lex intent recognition
- Publish and assign the flow to your claimed phone number

### 6. Set Up Routing
- Create queues (`PasswordReset`, `NetworkIssue`)
- Configure routing profiles and assign to users

### 7. Deploy and Test
- Use Amazon Connect's Test Chat and phone dial-in to simulate customer interaction
- Validate correct queue routing, voice prompts, and chatbot accuracy

---

## 🧪 Example Use Cases

| Intent         | User Says                             | Routed To         |
|----------------|----------------------------------------|-------------------|
| PasswordReset  | "I forgot my password"                | PasswordReset Queue |
| NetworkIssue   | "My internet is down"                 | NetworkIssue Queue |

---

## 📄 Documentation

All setup instructions, screenshots, and flow design diagrams are included in the [Amazon Connect Setup Guide (PDF)](./Amazon%20Connect%20Setup%20Guide.pdf).

---

## 🏁 Outcome

After completing this setup:
- Your AWS-based IT Help Desk will automatically respond to common queries using Lex bots
- Voice and chat requests will be routed intelligently to support queues
- Agents will be able to see what issue the caller is experiencing before picking up the call

---

## 🧠 Contributors

- Justin Haynes  
- Trevor Sobers  
- ITS Operations Center

---

## 🔒 License

This documentation is provided for educational and implementation use. Check AWS licensing and service policies for production use.
