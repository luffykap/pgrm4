pipeline {
    agent any

    tools {
        jdk 'jdk'
        maven 'maven'
    }

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Run') {
            steps {
                sh 'mvn exec:java -Dexec.mainClass="com.luffy.App"'
            }
        }

stage('Push Changes') {
    steps {
        withCredentials([
            usernamePassword(
                credentialsId: 'github-creds',
                usernameVariable: 'GITHUB_USER',
                passwordVariable: 'GITHUB_TOKEN'
            )
        ]) {
            sh '''
                git add destination.txt
                git commit -m "Update destination file" || true

                git push https://${GITHUB_USER}:${GITHUB_TOKEN}@github.com/luffykap/pgrm4.git HEAD:main
            '''
        }
    }
}
    }

    post {
        success {
            echo 'Build Successful ✅'
        }
        failure {
            echo 'Build Failed ❌'
        }
    }
}
