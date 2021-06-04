pipeline {
    agent {
        node {
            label 'orangesquadjenkinsslave-db2orders-did'
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
    }
}
