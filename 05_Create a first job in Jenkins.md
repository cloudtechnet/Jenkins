# Create a first job in Jenkins

In Jenkins, a **"Job"** (or **"Project"**) is a fundamental unit of work that defines what Jenkins will do. It could involve building a project, running tests, or deploying an application. The first job in Jenkins is typically a simple build process to understand how the platform works.

### Example: Hello World in Jenkins (Simple Build Job)

Let’s create a simple **"Hello World"** build job in Jenkins to understand how to set up and run your first Jenkins job.

### Step-by-Step Process

#### Step 1: Install Jenkins
First, ensure that Jenkins is installed and running on your server. You can access it via `http://localhost:8080` (or your server's IP and port).

#### Step 2: Create a New Job
1. On the Jenkins dashboard, click on the **"New Item"** link.
2. Enter a name for your job, e.g., **"HelloWorldJob"**.
3. Choose **"Freestyle project"** and click **OK**.

Freestyle projects are the most basic project type in Jenkins. They allow you to define simple builds and execute shell commands.

#### Step 3: Configure the Job
1. **Description**: Add a description for the job (optional). E.g., “This is my first Jenkins Hello World build job.”
   
2. **Source Code Management**: Since this is a basic example, we will skip SCM configuration.

3. **Build Triggers**: For this simple job, we won’t set up any automatic triggers like Git commits or time-based triggers. You can set this up later to automate your builds.

4. **Build Environment**: You can leave the default settings for now.

5. **Build Section**:
   - Scroll down to the **Build** section and click **Add build step**.
   - Choose **"Execute shell"** if you are on Linux/macOS, or **"Execute Windows batch command"** if you're on Windows.

6. **Add the Script**:
   - In the **"Execute shell"** section, write a simple command to echo "Hello World."
     ```bash
     echo "Hello World"
     ```

   - For Windows:
     ```cmd
     echo Hello World
     ```

#### Step 4: Save and Build
1. After configuring the job, click **Save** to save the project.
2. On the project’s page, click **Build Now**.

#### Step 5: Check the Build Output
1. After clicking **Build Now**, you’ll see the job appearing under the **Build History** section with a build number (e.g., `#1`).
2. Click on the build number to see the details of the build.
3. To check the console output, click **Console Output** on the left-hand side.

   The output should look something like this:
   ```
   Started by user admin
   Building in workspace /var/lib/jenkins/workspace/HelloWorldJob
   [HelloWorldJob] $ /bin/sh -xe /tmp/jenkins3971229489820728493.sh
   + echo Hello World
   Hello World
   Finished: SUCCESS
   ```

This output indicates that Jenkins executed the job and printed "Hello World" to the console.

### Summary
In this example:
- **Job Type**: Freestyle project.
- **Build Step**: We added a simple shell command to print "Hello World" to the console.
- **Result**: Jenkins ran the job successfully, showing the "Hello World" message in the console output.

This basic job demonstrates how Jenkins can execute simple tasks. From here, you can explore more advanced features like integrating source control (e.g., Git), setting build triggers, or automating tests and deployments.