pipeline {
    agent {
        node {
            label 'master'
        }
    }
    stages {
        stage('Versioning the app to Dev') {
            steps {
                script {
                  def pom = readMavenPom file: 'pom.xml'
                  printf("Version: %s", pom)
                }
            }
        }
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
