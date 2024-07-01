pipeline{
    agent {
        docker {
            image 'allbears/jenkins-android:1.0.1'
        }
    }

    parameters {
        string(name: 'GREETING', defaultValue: 'Hello', description: 'The greeting message')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'A boolean parameter')
        choice(name: 'CHOICE', choices: ['Option 1', 'Option 2', 'Option 3'], description: 'Choose an option')
    }

    stages {
        stage('Build'){
             steps {
                sh './gradlew clean && rm -rf ./app/build/'
                sh './gradlew assembleRelease'
             }
        }
       stage('UnitTest'){
             steps {
                sh './gradlew test'
             }
        }
        stage('Archive') {  
            steps {
                archiveArtifacts artifacts: 'app/build/outputs/**/*.apk', fingerprint: true 
            }
        }
    }

}