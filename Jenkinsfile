pipeline {

      agent any

      stages {

            stage('GIT') {

                  steps {

                        echo 'Hi, this is Hemant from 3Pillar'

                        echo 'We are Starting the Testing'
                        git 'https://github.com/HemantTomar/test.git'

                  }

            }
            stage('COMPILE_packege') {

                  steps {

                        echo 'COMPILE THE FILE'
                        tool name: 'Local_maven', type: 'maven'
                        sh 'mvn -f pom.xml package'
                        


                  }

            }

            stage('Build') {

                  steps {

                        echo 'Building Sample Maven Project'
                        archiveArtifacts '**/*.war'

                  }

            }
            stage('Test') {

                  steps {

                        echo 'Testing'
                       junit '**/target/surefire-reports/*.xml'
                        emailext body: '', recipientProviders: [upstreamDevelopers()], subject: 'hii', to: 'hemant14750@gmial.com'
                       

                  }

            }
            stage('Deploy') {

                  steps {

                        echo 'Deploying Sample Maven Project'
                        copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, projectName: 'pipeline', selector: lastWithArtifacts()
                        deploy adapters: [tomcat9(credentialsId: 'eb4b742d-2197-4c9e-9c71-07cd27a5a9b9', path: '', url: 'http://13.59.30.88:9090/')], contextPath: '/', war: '**/*.war'
                  }

            }


      }

}
