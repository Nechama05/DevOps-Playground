pipeline {
    agent any

    stages {
        stage('Init') {
            steps {
                // נותן לקובץ אישור ריצה (חובה בלינוקס)
                sh 'chmod +x gradlew'
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                // שימי לב: sh במקום bat, ונקודה-סלאש בהתחלה
                sh './gradlew clean build'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
                sh './gradlew test'
            }
        }

        stage('Run') {
            steps {
                echo 'Running App...'
                sh './gradlew run'
            }
        }
    }
}