pipeline{
  agent any
  stages{
    stage('build'){
          steps{
            sh 'mvn clean install'
          }
       }
    stage ("static code analis")
    {
      steps
      {
        script{
       withSonarQubeEnv(credentialsId: 'sonar') {
   sh 'mvn clean package sonar:sonar'
        }
        }
      }
    }
    stage ("upload war file to nexus")
    {
      steps
      {
        script{
          nexusArtifactUploader artifacts: 
            [
              [
                artifactId: 'my-app',
                classifier: '', file: 'target/my-app-1.0-SNAPSHOT.jar',
                type: 'jar']
            ],
            credentialsId: 'nexus',
            groupId: 'junit',
            nexusUrl: 'http://34.226.154.77:8081',
            nexusVersion: 'nexus2',
            protocol: 'http',
            repository: 'demo1', 
            version: '4.11'
        }
      }
    }
    // stage('Docker Image') {
     //        steps {
     //           script {
      //            sh 'docker build -t kajendran1451/my-app-1.0 .'
       //         }
       //     }
   //  }
   // stage('Docker deployment')
   // {
   // steps{
  // sh 'docker run -d -p 8025:8080 --name kaj1 kajendran1451/my-app-1.0 ' 
  //  }
   // }
}
}
