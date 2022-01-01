pipeline {
    agent any
    tools {
        maven 'maven'
    }

    environment {
        ArtifactId = readMavenPom().getArtifactId()
        Version = readMavenPom().getVersion()
        Name = readMavenPom().getName()
        GroupId = readMavenPom().getGroupId
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install package'
            }
        }

        stage('Test') {
            steps {
                echo "testing ....."
            }
        }

        stage('Publish to nexus') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab',
                classifier: '',
                file: 'target/VinayDevOpsLab-0.0.4-SNAPSHOT.war',
                type: 'war']],
                credentialsId: '632914b9-8d9c-48d8-beac-4854efd10fcd',
                groupId: 'com.vinaysdevopslab',
                nexusUrl: '10.123.2.116:8081',
                nexusVersion: 'nexus3',
                protocol: 'http',
                repository: 'VinayDevOpsLab-SNAPSHOT',
                version: '0.0.4-SNAPSHOT'
            }
        }

        stage('Print environment variables') {
            steps {
                echo "Artifact Id is '${ArtifactId}'"
                echo "Version is '${Version}'"
                echo "Name is '${Name}'"
                echo "GroupId is ${GroupId}"
            }
        }

        stage('Deploy') {
            steps {
                echo "deploying ...."
            }
        }
    }
}