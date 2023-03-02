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
//    stage ("upload war file to nexus")
  //  {
    //  steps
    //  {
      //  script{
          
        //  def readPomversion = readMavenPom file: 'pom.xml'
            
        //  nexusArtifactUploader artifacts: 
          //  [
            //  [
              //  artifactId: 'Train-Ticket', 
              //  classifier: '',
              //  file: 'target/TrainBook-0.0.1-SNAPSHOT.war',
             //   type: 'war'
            //  ]
           // ],
          //  credentialsId: 'nexus',
          //  groupId: 'TrainBook',
          //  nexusUrl: '44.202.23.92:8081',
          //  nexusVersion: 'nexus2',
           // protocol: 'http',
          //  repository: 'Train-Ticket',
          //  version: "${readPomVersion.version}"
    //  }
  //  }
  //  }
     stage('Docker Image') {
             steps {
                script {
                  sh 'docker build -t test/trainbook-0.0.1 .'
                }
            }
     }
    stage('Docker deployment')
    {
    steps{
  sh 'docker run -d -p 8014:8080 --name test test/trainbook-0.0.1 ' 
    }
    }
}
}
