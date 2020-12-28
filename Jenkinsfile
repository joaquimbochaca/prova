node ('ubuntu-app-agent'){  
    def app
    stage('Cloning Git') {
        /* Let's make sure we have the repository cloned to our workspace */
       checkout scm
    }  
   

    
    stage('Build-and-Tag') {
    /* This builds the actual image; synonymous to
         * docker build on the command line */
        app = docker.build("quimbochaca/prova:test")
        sh 'echo build-and-tag'
    }
     stage('SAST'){
    //    build 'SECURITY-SAST-SNYK'
    }
    stage('Post-to-dockerhub') {
    
     docker.withRegistry('https://registry.hub.docker.com', 'd050a934-7732-4ee2-9475-fdecc3bc07e7') {
            app.push("latest")
        		//	}
         }
    stage('SECURITY-IMAGE-SCANNER'){
        //build 'SECURITY-IMAGE-SCANNER-AQUAMICROSCANNER'
        sh 'echo security-image-scanner'
    }
  
    
    stage('Pull-image-server') {
    
         sh "docker-compose down"
         sh "docker-compose up -d"	
        sh 'echo pull-image-server'
      }
    
    stage('DAST')
        {
        //build 'SECURITY-DAST-OWASP_ZAP'
            sh 'echo DAST'
        }
 
}
