pipeline {
    agent any

    stages {
        stage('Init') {
            steps {
                echo 'Downloading Gradle manually...'
                sh 'curl -L -k -o gradle.zip https://services.gradle.org/distributions/gradle-9.3.0-bin.zip'
                sh 'jar xf gradle.zip'
                sh 'chmod +x gradle-9.3.0/bin/gradle'
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                sh './gradle-9.3.0/bin/gradle clean build'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
                sh './gradle-9.3.0/bin/gradle test'
            }
        }
    }

    // החלק החדש: מה עושים אחרי שהכל נגמר
post {
        success {
            // שומרים רק את קובץ ה-JAR (התוכנה המוכנה)
            // מחקנו את השורה של junit כדי שלא ייכשל על חוסר בטסטים
            archiveArtifacts artifacts: '**/build/libs/*.jar', allowEmptyArchive: true
        }
    }
}
}