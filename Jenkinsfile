pipeline {
    agent any

    tools {
        maven 'maven'
        jdk 'java'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ATZ-choosak/java-hello-world-with-maven']]])
            }
        }

        stage('Build') {
            steps {
                // Build and package the project using Maven
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // SonarQube analysis using Maven
                sh '''
                    mvn clean verify sonar:sonar \
                    -Dsonar.projectKey=coe6410110109 \
                    -Dsonar.projectName="coe6410110109" \
                    -Dsonar.host.url=http://172.17.0.3:9000 \
                    -Dsonar.login=sqp_1ec8b437191ad3e7d8f7c4efdee67fb8df58c7c0
                '''
            }
        }
    }
}
