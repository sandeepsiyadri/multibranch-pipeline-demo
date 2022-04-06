pipeline {

    agent {
        node {
            label 'master'
        }
    }
    
    options {
        buildDiscarder logRotator( 
                    daysToKeepStr: '16', 
                    numToKeepStr: '10'
            )
    }

    stages {
        
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                sh """
                echo "Cleaned Up Workspace For Project"
                """
            }
        }

        stage('Code Checkout') {
            steps {
                TAG_VERSION = sh(returnStdout: true, script: "git tag --contains").trim()
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: 'refs/tags/${TAG_VERSION}']], 
                    userRemoteConfigs: [[credentialsId: 'githubcred', url: 'https://github.com/sandeepsiyadri/multibranch-pipeline-demo.git']]
                ])
            }
        }

        stage(' Unit Testing') {
            steps {
                sh """
                echo "Running Unit Tests"
                """
            }
        }

        stage('Code Analysis') {
            steps {
                sh """
                echo "Running Code Analysis"
                """
            }
        }

        stage('Build Deploy Code') {
            when {
                branch 'develop'
            }
            steps {
                sh """
                echo "Building Artifact"
                """

                sh """
                echo "Deploying Code"
                """
            }
        }

    }   
}
