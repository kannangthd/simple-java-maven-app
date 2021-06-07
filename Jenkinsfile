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
                  def mvnHome = tool name: 'Maven', type: 'maven'  
                  sh "${mvnHome}/bin/mvn build-helper:parse-version versions:set \
                    -DnewVersion='\${parsedVersion.majorVersion}.\${parsedVersion.minorVersion}.\${parsedVersion.incrementalVersion}'"
                  sh '''
                     git add pom.xml
                     git commit -m "Uploading the newly updated version on github repo under master branch"
                     git push
                    '''
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
