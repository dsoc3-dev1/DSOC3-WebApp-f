pipeline{
    agent { label 'agent-1'}
    parameters{
        // String parameter for specifying a custom branch
       string(
            name:'BRANCH', 
            defaultValue:'main',
            description: 'Branch to Deploy'
        )
        // Choice parameter for selecting the environment
       choice(
           name: 'ENVIRONMENT',
           choices: ['dev', 'test', 'stage', 'prod'],
           description: 'Select the environment to deploy to'
       )
    }

    tools{
       maven 'Maven 3.9.9'
   }
    stages{
        stage('Parallel Stages'){
            parallel {
                    stage('Build'){
                        steps{
                            echo 'Building the DSOC3 WEB APP..'
                            //echo "GIT_BRANCH: ${env.GIT_BRANCH}"
                            sh 'mvn -v'
                        sh '''
                         ls -lrt
                         mvn compile test package
                        '''
                            
                        }
                    }//EO Build
                    /*stage('Test'){
                        tools{
                            maven 'DSOC3'
                        }
                        steps{
                            echo 'Testing the DSOC3 WEB APP..'
                            sh 'mvn -v'
                        }
                    }//EO Test*/

            }
        }//EO Parallel Stages    
        stage('Deploy'){
            /*when {
                expression {
               //return env.GIT_BRANCH == 'origin/test'
               //return params.BRANCH == 'test'
               return params.BRANCH == 'test2' && (params.ENVIRONMENT == 'stage' || params.ENVIRONMENT == 'prod')
                }

            }*/
            steps{
                //echo 'Deploying the DSOC3 WEB APP..'
                echo "Deploying...from branch ${params.BRANCH}"
                sh '''
                sudo cp target/dsoc3-webapp.war /var/lib/tomcat10/webapps/dsoc3-webapp.war
                '''
            }
        }//EO Deploy
        
    }
}
