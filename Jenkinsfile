node ('maven-label') {
    def mvnHome
    stage('Preparation') { // for display purposes
        // Get some code from a GitHub repository
        git 'https://github.com/rehana-suhail/Hello_Java.git'
        // Get the Maven tool.
        // ** NOTE: This 'M3' Maven tool must be configured
        // **       in the global configuration.
        mvnHome = tool 'maven-3.5.2'
        //latest maven tool
        //hello
    }
    stage('Build') {
        // Run the maven build
        withEnv(["MVN_HOME=$mvnHome"]) {
            if (isUnix()) {
                //sonar added just try
                sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package sonar:sonar -Dsonar.host.url="http://ec2-13-233-126-127.ap-south-1.compute.amazonaws.com:9000"'
            } else {
                bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
            }
        }
    }
    stage('Results') {
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts 'target/*.jar'
    }
}
