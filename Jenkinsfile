pipeline {
    agent {
        node {
            label 'master'
        }
    }
    stages {
        stage('Build') { 
            steps {
                script {
                    def mvnHome = tool name: 'Maven', type: 'maven'
                    sh "${mvnHome}/bin/mvn -version"
                    sh "${mvnHome}/bin/mvn -B -DskipTests clean package"
                }
            }
        }
    }
}
