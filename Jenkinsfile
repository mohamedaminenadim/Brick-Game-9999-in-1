pipeline {
    agent any

    tools {
        // Install JDK and Maven
        jdk 'jdk8'
        maven 'Maven'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout source code from Git repository
                git 'https://github.com/mohamedaminenadim/Brick-Game-9999-in-1'
            }
        }

        stage('Build') {
            steps {
                // Build the Maven project
                sh 'mvn clean package -DskipTests'
            }

            post {
                success {
                    // Archive the built JAR file
                    archiveArtifacts 'target/*.jar'
                }
            }
        }

        stage('Unit Tests') {
            steps {
                // Run unit tests
                sh 'mvn test'
            }
        }

        stage('Package Generation') {
            steps {
                // Generate additional artifacts (e.g., Javadoc, source code)
                sh 'mvn javadoc:javadoc'
                sh 'mvn source:jar'
            }

            post {
                // Archive additional artifacts
                archiveArtifacts 'target/site/apidocs/**'
                archiveArtifacts 'target/*.jar'
                archiveArtifacts 'target/*.jar.asc'
            }
        }

        stage('Save Artifacts') {
            steps {
                // Save any necessary artifacts
                sh 'mvn install -DskipTests'
            }

            post {
                // Archive additional artifacts
                archiveArtifacts 'target/*.pom'
                archiveArtifacts 'target/*.pom.asc'
                archiveArtifacts 'target/*.md5'
                archiveArtifacts 'target/*.sha1'
            }
        }

        stage('Publish Package') {
            when {
                // Condition to publish the package (if required)
                branch 'master'
            }
            steps {
                // Publish package to Maven repository
                sh 'mvn deploy'
            }
        }

        stage('Additional Steps') {
            steps {
                // Add any additional steps you deem necessary
                sh "echo Pipeline completed succesfully"
            }
        }
    }
}
