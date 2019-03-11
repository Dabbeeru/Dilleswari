       pipeline {
          agent any
          stages {
              stage('Checkout external proj') {
                steps {
                    git branch: 'master',
                        credentialsId: 'gitlab',
                    url: 'https://github.com/Dabbeeru/Dilleswari.git'
        
                    sh "ls -lat"
			sh mvnHome = tool 'M3'

        bat "${mvnHome}\\bin\\mvn -B install"
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
                sh 'mvn -f otherdirectory/pom.xml clean install ' 
            }

  }
 
    

 stage('Create Docker Image') {
 steps{
    dir('webapp') {
       
	   sh docker.build("dilleswari/docker-jenkins-pipeline:${env.BUILD_NUMBER}")
	  
    }
  }
}
  stage ('Run Application') {
  steps{
    
      // Start database container here
      // sh 'docker run -d --name db -p 8091-8093:8091-8093 -p 11210:11210 dilleswari/oreilly-couchbase:latest'

      // Run application using Docker image
      sh "DB=`docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' db`"
      sh "docker run -e DB_URI=$DB dilleswari/docker-jenkins-pipeline:${env.BUILD_NUMBER}"

      // Run tests using Maven
      //dir ('webapp') {
      //  sh 'mvn exec:java -DskipTests'
      //}
    } 
	
  
}
  stage('Run Tests') {
  steps{
    
      dir('webapp') {
        sh "mvn test"
       sh docker.build("dilleswari/docker-jenkins-pipeline:${env.BUILD_NUMBER}").push()
      }
    }  
 
}
    }

}
