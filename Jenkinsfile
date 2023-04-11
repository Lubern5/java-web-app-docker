node{
    
    stage(" Maven Clean Package"){
      def mavenHome =  tool name: "Maven-3.9.1", type: "maven"
      def mavenCMD = "${mavenHome}/bin/mvn"
      sh "${mavenCMD} clean package"
      
    } 
    
    
   stage('Push Docker Image'){
        withCredentials([string(credentialsId: 'Docker_Hub', variable: 'Docker_Hub')]) {
          sh "docker login -u lubern5 -p ${Docker_Hub}"
        }
        sh 'docker push lubern5/java-web-app'
     }
     
      stage('Run Docker Image In Dev Server'){
        
        def dockerRun = ' docker run  -d -p 8080:8080 --name java-web-app lubern5/java-web-app'
       
    }
     
     
}
