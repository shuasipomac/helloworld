pipeline {
    agent any

     stages {

        stage('Hello') {
           steps {
              echo 'Hello World'	 
              }
           }

        stage('Get Code') {
            steps {
                // Trae todo el código fuente del repositorio
                git 'https://github.com/shuasipomac/helloworld.git'
            }
        }

        stage('Build') {
           steps {
              echo 'No hay código para compilar'
	      echo WORKSPACE
              bat 'dir'
           }
        }

         
stage ('Test') {
parallel {

       stage('Unit') {
            steps {
                catchError(buildResult: 'UNSTABLE', stageResult: 'FAILURE') {
                    bat '''
                        set PYTHONPATH=%WORKSPACE%
                        C:\Python\Python312\Scripts\pytest test\\unit
                    '''
                    }
                  }
               }   


        stage('Rest') {
            steps {
                catchError(buildResult: 'UNSTABLE', stageResult: 'FAILURE') {

                bat '''
                    set FLASK_APP=app\\api.py
                    set FLASK_ENV=development
                    start flask run
                    start java -jar C:\\Unir\\Ejercicios\\wiremock\\wiremock-jre8-standalone-2.28.0.jar --port 9090 --root-dir C:\\Unir\\Ejercicios\\wiremock
                    
                    set PYTHONPATH=%WORKSPACE%
                    pytest --junitxml=result-rest.xml test\\rest
                '''
                   }    
                  }
                 }

             }
         }
        
stage('Results') {
            steps {
                junit 'result*.xml' 
            }
        }


     }
}
