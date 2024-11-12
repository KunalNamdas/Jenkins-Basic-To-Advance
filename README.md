# **Jenkins Guide: From Basics to Advanced Usage**

## **Chapter 1: Introduction to Jenkins**

### **What is Jenkins?**
Jenkins is a widely-used, open-source automation tool written in Java that facilitates continuous integration (CI) and continuous delivery (CD) in software projects. It helps automate repetitive tasks like building, testing, and deploying software.

#### **Why Use Jenkins?**
- **Automation**: Automates tasks like code integration, testing, and deployment.
- **Consistency**: Ensures consistent builds and releases.
- **Integration**: Easily integrates with popular tools such as Git, Docker, Maven, and AWS.
- **Scalability**: Scalable to meet the needs of large teams and enterprises.
- **Extensibility**: With over 1,500 plugins, Jenkins can be customized to meet specific project needs.

---

## **Chapter 2: Benefits of Using Jenkins**

### **Key Benefits of Jenkins:**
1. **Time-Saving**: Jenkins automates tedious tasks, speeding up the development lifecycle.
2. **Improved Quality**: Jenkins ensures automated testing, making it easier to catch bugs early.
3. **Continuous Integration**: Developers can merge code into the repository frequently, leading to faster integration and feedback.
4. **Early Detection of Issues**: Automated testing helps catch bugs early in the development cycle.
5. **Cost-Effective**: Reduces manual work, which saves time and costs in the long run.

---

## **Chapter 3: Installing Jenkins**

### **Step 1: Install Java (Prerequisite)**

Since Jenkins is built in Java, you must install Java first.

#### For Windows:
1. **Download**: Visit the [Oracle website](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) to download Java.
2. **Install**: Run the installer and follow the instructions.
3. **Verify**: Open Command Prompt and type:
   ```bash
   java -version
   ```

#### For Linux (Ubuntu/Debian):
```bash
sudo apt update
sudo apt install openjdk-11-jdk
java -version
```

#### For macOS:
```bash
brew install openjdk@11
```

### **Step 2: Install Jenkins**

#### For Windows:
1. **Download Jenkins** from the [Jenkins website](https://www.jenkins.io/download/).
2. **Run the Installer**: Follow the instructions.
3. **Access Jenkins**: Open your browser and go to `http://localhost:8080`.

#### For Linux (Ubuntu/Debian):
1. **Add Jenkins Repository**:
   ```bash
   wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee \
   /etc/apt/trusted.gpg.d/jenkins.asc
   ```

2. **Install Jenkins**:
   ```bash
   sudo sh -c 'echo deb http://pkg.jenkins.io/debian/ stable main > \
   /etc/apt/sources.list.d/jenkins.list'
   sudo apt update
   sudo apt install jenkins
   ```

3. **Start Jenkins**:
   ```bash
   sudo systemctl start jenkins
   ```

#### For macOS:
```bash
brew install jenkins-lts
brew services start jenkins-lts
```

### **Step 3: Access Jenkins**
Once Jenkins is installed and running, open your browser and visit [http://localhost:8080](http://localhost:8080).

---

## **Chapter 4: Unlock Jenkins**

1. **Find the Initial Password**:
   - On Linux: 
     ```bash
     sudo cat /var/lib/jenkins/secrets/initialAdminPassword
     ```
   - On Windows, the password is located at `C:\Program Files (x86)\Jenkins\secrets\initialAdminPassword`.

2. **Enter the Password**: Copy and paste the password into the Jenkins setup screen.

---

## **Chapter 5: First Time Setup and Plugin Installation**

Jenkins will prompt you to install suggested plugins during the first setup. It’s recommended to install these plugins to get started quickly. These plugins help Jenkins interact with source control systems like Git, build systems like Maven, and notification services like Slack.

### **Install Suggested Plugins**:
Click the **Install suggested plugins** option.

### **Add Plugins Manually**:
If you need a specific plugin:
1. Go to **Manage Jenkins** > **Manage Plugins**.
2. Search for the plugin and install it.

---

## **Chapter 6: Jenkins Job Creation and Configuration**

### **What is a Jenkins Job?**
A job is a single task that Jenkins performs. Jobs automate tasks like building, testing, and deploying applications.

### **Creating a Job**:
1. **Go to Jenkins Dashboard** and click **New Item**.
2. Enter a name for your job.
3. Choose the type of job (e.g., **Freestyle project**, **Pipeline**).
4. Click **OK**.

### **Job Configuration**:
- **Source Code Management**: Link your job to a GitHub or GitLab repository.
- **Build Triggers**: Configure triggers to start the job automatically (e.g., after code commits or on a schedule).
- **Build Steps**: Define the steps Jenkins will take (e.g., running tests, compiling code).
- **Post-build Actions**: Actions after the build, like sending notifications or deploying the code.

---

## **Chapter 7: Jenkins Pipeline Basics**

A **Pipeline** in Jenkins is a series of automated steps that define how to build, test, and deploy your code.

### **Declarative Pipeline Example**:
```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
            }
        }
    }
}
```

### **How to Create a Pipeline Job**:
1. Select **Pipeline** job type when creating a new item.
2. In the job configuration, paste the pipeline script into the **Pipeline Script** section.
3. Save and run the job.

---

## **Chapter 8: Jenkins and Docker Integration**

Jenkins can integrate seamlessly with Docker to build, test, and deploy applications inside Docker containers.

### **Example: Build Docker Image in Jenkins Pipeline**:
```groovy
pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('my-app')
                }
            }
        }
    }
}
```

### **How to Use Jenkins for Docker Builds**:
1. Install the **Docker Plugin**.
2. Add Docker commands within your Jenkins pipeline to build and run Docker containers.

---

## **Chapter 9: Jenkins Distributed Builds with Nodes**

Jenkins can distribute tasks to other machines, called **nodes**, to speed up builds. This is useful in large teams or projects with multiple environments (e.g., testing, staging, production).

### **Adding a New Node**:
1. Go to **Manage Jenkins** > **Manage Nodes**.
2. Click **New Node**, enter a name, and select **Permanent Agent**.
3. Follow the setup instructions to link the new node.

---

## **Chapter 10: Advanced Jenkins Usage**

### **1. Jenkins and Version Control**:
Jenkins integrates with version control systems like **Git** and **SVN**. This allows Jenkins to automatically trigger builds when code changes are committed to the repository.

#### **Configuring Git in Jenkins**:
1. Install the **Git Plugin**.
2. In your job configuration, link the job to your Git repository URL.
3. Set triggers for build actions based on commits or pull requests.

### **2. Jenkins Notifications**:
Jenkins can send notifications about job statuses via email, Slack, or other tools. This keeps team members informed about the state of their builds.

#### **Configuring Email Notifications**:
1. Go to **Manage Jenkins** > **Configure System**.
2. Add email notification settings (SMTP server, from address, etc.).
3. In job configuration, set **Post-build Actions** to send notifications.

---

## **Chapter 11: Jenkins Security**

### **Securing Jenkins**:
1. **Enable Security**: Go to **Manage Jenkins** > **Configure Global Security**.
2. Enable **Jenkins’ own user database** for authentication.
3. Assign roles to users to manage access.

### **Backup and Restore Jenkins**:
- **Backup**: Periodically backup Jenkins configurations and jobs using the **ThinBackup Plugin**.
- **Restore**: Use the same plugin to restore the backup in case of a disaster.

---

## **Conclusion**

Jenkins is a powerful tool that can automate software development processes, making it easier to integrate, test, and deploy applications. By following this guide, you can start using Jenkins for continuous integration, improve your development workflow, and deploy applications more efficiently.

---

**Designed by Kunal Namdas**

---
