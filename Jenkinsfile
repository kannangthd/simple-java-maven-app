pipeline {
    agent {
        node {
            label 'master'
        }
    }
    stages {
        stage('Versioning the app to Stage') {
            when {
                branch 'master'
            }
            steps {
                script {
                  def pom = readMavenPom file: 'pom.xml'
                  printf("Version: %s", pom.version)
                  version = getVersion(pom)
                  printf("Version again: %s", version)
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
