# change the artifact version ID randomly

In Jenkins, to change the artifact version ID randomly for each build, you can use Jenkins pipeline scripts with either a Groovy function to generate a random version or rely on the `BUILD_ID` or `BUILD_NUMBER` Jenkins environment variables to create unique version IDs for each build.

Here’s a step-by-step guide:

### Step 1: Configure Your Pipeline Job

1. Open Jenkins and go to your job configuration.
2. In the **Pipeline** section, select **Pipeline script** to use a scripted or declarative pipeline.

### Step 2: Create a Random Version ID

You can define a random version ID in your Jenkinsfile or inline pipeline script by creating a Groovy function or directly using the Jenkins `BUILD_ID` variable.

Here’s how to do it:

- **Using a Random Function**: You can generate a random string or number.
- **Using Jenkins `BUILD_ID` or `BUILD_NUMBER`**: These are unique to each build and ensure your version ID changes each time.

### Example Pipeline Script

This script creates a random version ID by appending a random number to the base version or using `BUILD_ID`.

```groovy
pipeline {
    agent any

    environment {
        // Base version format
        BASE_VERSION = "1.0.0"
    }

    stages {
        stage('Generate Random Version') {
            steps {
                script {
                    // Option 1: Use a random number for the version
                    def randomId = new Random().nextInt(1000)
                    env.VERSION_ID = "${BASE_VERSION}-${randomId}"

                    // Option 2: Use Jenkins BUILD_ID
                    env.VERSION_ID = "${BASE_VERSION}-${env.BUILD_ID}"

                    // Print the generated version ID
                    echo "Generated Artifact Version: ${env.VERSION_ID}"
                }
            }
        }
        
        stage('Build and Package') {
            steps {
                script {
                    // Example: Update your Maven or Gradle build command
                    sh "mvn clean package -Dartifact.version=${env.VERSION_ID}"
                    // or
                    sh "gradle build -PartifactVersion=${env.VERSION_ID}"
                }
            }
        }

        stage('Publish Artifact') {
            steps {
                script {
                    echo "Publishing artifact with version: ${env.VERSION_ID}"
                    // Upload artifact with version to repository, e.g., Nexus or Artifactory
                }
            }
        }
    }
}
```

### Step 3: Use the Version ID in Artifact Name

1. In the **Build and Package** stage, pass the generated `VERSION_ID` to your build tool.
2. Update the artifact naming convention to use `${VERSION_ID}`.

### Step 4: Run the Pipeline and Verify

1. Save your pipeline script and trigger a build.
2. Check the console output to verify that each build produces a unique artifact version ID. 

