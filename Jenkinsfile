pipeline {
    agent any

    stages {
        stage('Init') {
            steps {
                echo 'Downloading Gradle manually (ignoring SSL)...'
                // 1. הורדה אגרסיבית עם curl (הדגל -k אומר להתעלם מ-SSL)
                sh 'curl -L -k -o gradle.zip https://services.gradle.org/distributions/gradle-9.3.0-bin.zip'

                // 2. חילוץ הקובץ (שימוש ב-jar כי unzip לא תמיד קיים)
                sh 'jar xf gradle.zip'

                // 3. מתן הרשאות ריצה
                sh 'chmod +x gradle-9.3.0/bin/gradle'
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                // שימי לב: אנחנו מריצים את הגריידל שהורדנו הרגע, לא את ה-wrapper
                sh './gradle-9.3.0/bin/gradle clean build'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
                sh './gradle-9.3.0/bin/gradle test'
            }
        }

        stage('Run') {
            steps {
                echo 'Running App...'
                sh './gradle-9.3.0/bin/gradle run'
            }
        }
    }
}