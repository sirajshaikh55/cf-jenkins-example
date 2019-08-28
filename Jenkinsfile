pipeline{
    agent any

    stages {
        stage('Build') {
            steps {
                withMaven(maven: 'MAVEN') {
                    sh 'mvn clean package'
                }
            }
        }

        stage ('Deploy') {
            steps {

                withCredentials([[$class: UsernamePasswordMultiBinding,
                                  credentialsId: 'PCF_LOGIN',
                                  usernameVariable: 'USERNAME',
                                  passwordVariable: 'PASSWORD']]) {

                     bat 'C:/Program Files/Cloud Foundry/cf login -a http://api.run.pivotal.io -u $USERNAME -p PASSWORD'
                     bat 'C:/Program Files/Cloud Foundry/cf push'
                                  }
            }
        }
    }
}