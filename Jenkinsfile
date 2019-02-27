    node {
    def mvnHome
    stage('Tool Setup') {  
        mvnHome = tool 'mvn'
    }

    stage('Checkout') {

        checkout([$class: 'GitSCM', branches: [[name: '*/master']], 
        doGenerateSubmoduleConfigurations: false, 
        extensions: [],
        submoduleCfg: [], 
        userRemoteConfigs: [[url: 'https://github.com/abhinav9292/devops-web-hackathon.git']]])
    
    }
    stage('Build') {
        // Run the maven build
        if (isUnix()) {
            sh "'${mvnHome}/bin/mvn'  clean package"
        } else {
            bat(/"${mvnHome}\bin\mvn" clean package/)
        }
    }
    
    stage('Upload Artifact') {
        sh script: 'curl -uadmin:armareddy -T ${WORKSPACE}/target/*.jar http://localhost:8081/artifactory/example-repo-local/devops-web-hackathon/DEV_ENV/${BUILD_NUMBER}/'
    }
    
    stage('Download Artifact') {
        dir('../../userContent') {
        sh script: 'curl -uadmin:armareddy -O  http://localhost:8081/artifactory/example-repo-local/devops-web-hackathon/DEV_ENV/${BUILD_NUMBER}/${BUILD_NUMBER}-devops-web-hackathon-1.0.jar'
    }
        sh script: 'curl -uadmin:armareddy -O  http://localhost:8081/artifactory/example-repo-local/devops-web-hackathon/DEV_ENV/${BUILD_NUMBER}/${BUILD_NUMBER}-devops-web-hackathon-1.0.jar'
    }
    
    
    
    }
