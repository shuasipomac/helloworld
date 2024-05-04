pipeline {
    agent any

     stages {
       
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

    
       stage ('Tests') {
       parallel {

       stage('Unit') {
            steps {
                catchError(buildResult: 'UNSTABLE', stageResult: 'FAILURE') {
                    bat '''
                        set PYTHONPATH=%WORKSPACE%
			set path=C:\\Python\\Python312;C:\\Python\\Python312\\Scripts;
                        pytest --junitxml=result-unit.xml test/unit
                    '''
                    }
                  }
               }   

   
        stage('Rest') {
            steps {
                catchError(buildResult: 'UNSTABLE', stageResult: 'FAILURE') {
                bat '''                         
                    set FLASK_APP=app\\api.py
                    
                    start Java -jar C:\\CLON\\wiremock\\wiremock-standalone-3.5.3.jar --port 9090 --root-dir test\\wiremock

                    set PYTHONPATH=%WORKSPACE%  
                    pytest --junitxml=result-rest.xml test/rest
                '''
                   }    
                  }
                 }

             }
         }


         stage('Results') {
            steps {
                junit 'result*.xml' 
                echo 'FINISH!!!'
                 }
            }


     }
}
