Project Overview
This project delivers an enterprise-grade test automation infrastructure deployed entirely on the cloud. It demonstrates the transition from local testing to a remote, distributed, and containerized environment using AWS EC2, Docker, and Jenkins.

It eliminates the classic “works on my machine” problem by providing a standardized, reproducible execution environment in the cloud.

🏗️ Architecture
Flow: GitHub (Source) → Jenkins (CI/CD) → AWS EC2 (Host) → Docker Compose → Selenium Hub & Nodes

🔑 Key Features
☁️ AWS Cloud Native: Hosted on a high-performance EC2 (c5a.2xlarge) instance.

🐳 Docker Orchestration: docker-compose.yml spins up Selenium Hub and dynamic browser nodes (Chrome, Firefox, Edge).

⚡ Parallel Execution: Achieved ~50% faster test runs by scaling browser nodes dynamically.

🔄 CI/CD Integration: Declarative Jenkins Pipeline automates the lifecycle: Pull Code → Start Infrastructure → Run Tests → Generate Reports → Tear Down.

🛡️ Zero Local Dependency: Tests run entirely on the remote server, freeing local resources.

🛠️ Tech Stack
Component	Tool / Technology
Language	Java 21 (Amazon Corretto)
Automation	Selenium WebDriver 4
Framework	Cucumber BDD + TestNG
Containers	Docker & Docker Compose
CI/CD	Jenkins (Pipeline as Code)
Cloud	AWS (Amazon Linux 2023)
Reporting	Extent Reports & Cucumber HTML
⚙️ Infrastructure as Code (IaC)
The grid configuration is fully defined in docker-compose.yml, ensuring reproducibility and scalability.

Snippet:

yaml
services:
  selenium-hub:
    image: selenium/hub:latest
    ports:
      - "4444:4444"

  chrome:
    image: selenium/node-chrome:latest
    depends_on:
      - selenium-hub
    environment:
      - SE_EVENT_BUS_HOST=selenium-hub
      - SE_NODE_MAX_SESSIONS=2
🚀 How to Execute
Method 1: Jenkins Pipeline (Recommended)
Trigger Build Now in Jenkins.

Pipeline provisions Docker containers on AWS.

Tests execute in parallel across Chrome, Firefox, and Edge.

Reports are archived as Jenkins artifacts.

Method 2: Manual Execution (EC2 / Local)
bash
# 1. Spin up the Grid
docker compose up -d --scale chrome=2 --scale firefox=2

# 2. Trigger Tests
mvn clean test

# 3. Stop Infrastructure
docker compose down
📊 Reports
Cucumber Overview Report: Scenario breakdown for BDD.



👤 Author
Sanjay Mahanta QA Automation Engineer & DevOps Enthusiast

🔗 Connect on LinkedIn
https://www.linkedin.com/in/sanjaymahanta28/
