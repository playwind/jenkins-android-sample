pipeline{
    agent {
        docker {
            image 'allbears/jenkins-android:1.0.1'
            label 'jenkins-android'
        }
    }

    parameters {
        string(name: 'version_name', defaultValue: 'v1.0', description: 'build version')
        choice(name: 'build_type', choices: ['Debug', 'Release'], description: 'build type')
    }

    stages {
        stage('Build'){
             steps {
                sh './gradlew clean && rm -rf ./app/build/'
                sh "./gradlew assemble${params.build_type}"
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