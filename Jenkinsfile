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
                  printf("Version: %s", pom.version)
                  sh mvn build-helper:parse-version versions:set \
                    -DnewVersion=\${parsedVersion.majorVersion}.\${parsedVersion.minorVersion}.\${parsedVersion.incrementalVersion}  
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
