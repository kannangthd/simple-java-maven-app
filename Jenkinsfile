pipeline {
    agent {
        node {
            label 'master'
        }
    }
    stages {
        stage('Build') { 
            steps {
                // Run Maven on a Unix agent.
                def mvnHome = tool name: 'Maven', type: 'maven'
                sh "${mvnHome}/bin/mvn -version"
                sh 'mvn -B -DskipTests clean package'
            }
        }
    }
}
