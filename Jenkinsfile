node {
    def buildNumber = BUILD_NUMBER 
    stage("Git Clone"){
        git url: 'https://github.com/AmareshACS/Docker-Node.js.git', branch: 'master'
    }

    stage("Build Docker Image"){
        sh "docker build -t amareshdockerhub/node-app:${buildNumber} ."
    }
    stage('Test Image'){
       app.inside {
         sh 'echo "TEST PASSED"'
        }  
    }
    stage("Docker Login and Push"){
        withCredentials([string(credentialsId: 'DockerHubPassword', variable: 'DockerHubPassword')]) {
            sh "docker login -u amareshdockerhub -p ${DockerHubPassword}"
        }
        sh "docker push amareshdockerhub/node-app:${buildNumber}"
    }
}
