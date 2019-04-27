 pipeline {
        environment {
    registry = "dilleswari/learning"
    registryCredential = 'Dockerhub'
  }
          agent any
          stages {
              stage('Checkout external proj') {
                steps {
                    git branch: 'master',
                        credentialsId: 'gitlab',
                    url: 'https://github.com/Dabbeeru/Dilleswari.git'
        
                    sh "ls -lat"
                }
        		}
        	
            
              
            
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }

        stage ('Build') {
            steps {
                sh 'mvn clean package -DskipTests' 
            }

  }
 
    


  
  stage('Run Tests') {
     
      steps ('webapp') {
        sh "mvn  -fae test"
         
      }
     
     
  }
    }

}
