node{
     
    stage('SCM Checkout'){
        git url: 'https://github.com/Devops-13999/Java_webapp.git',branch: 'master'
    }
    
    stage(" Maven Clean Package"){
      def mavenHome =  tool name: "Maven", type: "maven"
      def mavenCMD = "${mavenHome}/bin/mvn"
      sh "${mavenCMD} clean install"
    } 
    
    stage('Build Docker Image'){
        sh 'docker build -t shiksha0102/java-app-container-jen:version1 .'
    }
    
    stage('Push Docker Image'){
        withCredentials([usernamePassword(
            credentialsId: "Docker",
            usernameVariable: "USER",
            passwordVariable: "PASS"
    )]) {
        sh "docker login -u '$USER' -p '$PASS'"
    }
    sh "docker image push shiksha0102/java-app-container-jen:version1"
    }
    stage('Run Docker Image In Dev Server'){
        
        def dockerRun = ' docker run  -d -p 8080:8080 --name java-web-app shiksha0102/java-app-container-jen:version1'
         
         sshagent(['ssh_agent']) {
          sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.2.232 docker stop java-web-app || true'
          sh 'ssh  ubuntu@172.31.2.232 docker rm java-web-app || true'
          sh 'ssh  ubuntu@172.31.2.232 docker rmi -f  $(docker images -q) || true'
          sh "ssh  ubuntu@172.31.2.232 ${dockerRun}"
       }
       
    }
    
  
}
