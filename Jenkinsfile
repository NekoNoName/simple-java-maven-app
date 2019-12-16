pipeline {
    agent any //{
        //docker {
          //  image 'maven:3-alpine'
            //args '-v /root/.m2:/root/.m2'
        //}
    //}
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                  withSonarQubeEnv('GLW SonarQube Server') {
                sh 'mvn sonar:sonar'
                  }
            }
            
        }
        stage('Deliver') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
            }
        }
    }
}
