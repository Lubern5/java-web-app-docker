node{
    
    stage(" Maven Clean Package"){
      def mavenHome =  tool name: "Maven-3.5.6", type: "maven"
      def mavenCMD = "${mavenHome}/bin/mvn"
      sh "${mavenCMD} clean package"
      
    } 
    
    
    stage('Build Docker Image'){
        sh 'docker build -t lubern5/java-web-app .'
    }
    
    stage('Push Docker Image'){
        withCredentials([string(credentialsId: 'Docker_Hub_Pwd', variable: 'Docker_Hub_Pwd')]) {
          sh "docker login -u lubern5 -p ${Docker_Hub_Pwd}"
        }
        sh 'docker push lubern5/java-web-app'
     }
     
      stage('Run Docker Image In Dev Server'){
        
        def dockerRun = ' docker run  -d -p 8080:8080 --name java-web-app dockerhandson/java-web-app'
         
         sshagent(['DOCKER_SERVER']) {
          sh 'ssh -o StrictHostKeyChecking=no ubuntu@18.188.39.190 docker stop java-web-app || true'
          sh 'ssh  ubuntu@18.188.39.190 docker rm java-web-app || true'
          sh 'ssh  ubuntu@18.188.39.190 docker rmi -f  $(docker images -q) || true'
          sh "ssh  ubuntu@18.188.39.190 ${dockerRun}"
       }
       
    }
     
     
}
