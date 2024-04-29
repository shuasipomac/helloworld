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

     }
}
