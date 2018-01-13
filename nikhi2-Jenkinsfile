pipeline {
    agent any 

    stages {
        stage('Build') { 
            environment {
                 JAVA_HOME = tool 'jdk-8u45'
                 PATH="${JAVA_HOME}/bin:${PATH}"
                 MAVEN_HOME = tool 'M3'
            }
            steps { 
                sh '${MAVEN_HOME}/bin/mvn -U clean test cobertura:cobertura -Dmaven.test.skip=true -Dcobertura.report.format=xml' 
            }
        }
        stage('NexusArtifactUploaderJob') {
            steps {
              nexusArtifactUploader artifacts: [[artifactId: 'nexus-artifact-uploader', classifier: 'debug', file: 'nexus-artifact-uploader.jar', type: 'jar']], credentialsId: 'nexus', groupId: 'sd.sd', nexusUrl: '172.17.0.2:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-releases', version: '2'
            }
       }
    }
}
