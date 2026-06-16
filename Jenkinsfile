
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
      
        stage('Commit Changes') {
    stage('Push Changes') {
    steps {
        sh '''
            git checkout main

            git config user.email "luffykapill@gmail.com"
            git config user.name "luffykap"

            git add destination.txt
            git commit -m "Update destination file" || true

            git push origin main
        '''
    }
}
    }}

    post {
        success {
            echo 'Build Successful ✅'
        }
        failure {
            echo 'Build Failed ❌'
        }
    }
}
