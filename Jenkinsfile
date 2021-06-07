pipeline {
    agent {
        node {
            label 'master'
        }
    }
    stages {
        stage('Code Checkout') {
            steps {
                script {
                    sh '''
                        git remote -v
                        git remote rm origin
                        git remote add origin "https://github.com/kannangthd/simple-java-maven-app.git"
                    '''
                }
            }
        }
        stage('Determination of Build Type') {
          steps {
            script {
                if (env.GIT_BRANCH == "master") {
                 echo "Build type is Master"
                 env.deploy_env = "stage"
               } else if (env.GIT_BRANCH == "dev-master"){
                 echo "Build type is DEV"
                 env.deploy_env = "dev"
               } else if (env.GIT_BRANCH.contains("-dev")) {
                 echo "Build type is Feature branch"
                 env.deploy_env = "feature"
               } else if (env.GIT_BRANCH.contains("bugfix")) {
                 echo "Build type is Feature branch"
                 env.deploy_env = "bugfix"
              } 
            }
          }
        }
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
