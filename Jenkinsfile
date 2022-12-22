pipeline{
    agent any
    tools {nodejs "nodejs"}
    stages{
        stage('code checkout from GitHub'){
            steps{
                git 'https://github.com/revm19/nodejsboilerplatecode.git'
            }
        }
        stage('Code Quality Check via SonarQube'){
            steps{
                script{
                    def scannerHome = tool 'sonarqube-scanner';
                    withSonarQubeEnv(credentialsId: 'sonarqube_access_token'){
                        sh "${tool("sonarqube-scanner")}/bin/sonar-scanner \
                        -Dsonar.projectKey=devopstest \
                        -Dsonar.sources=. \
                        -Dsonar.css.node=. \
                        -Dsonar.host.url=http://10.20.2.174:9000/ \
                        -Dsonar.login=678f105542297ae045c501ffc230d0a4a9b2214a"
                        
                    }
                }
            }
        }
        stage('Install Project Dependencies'){
            steps{
                nodejs(nodeJSInstallationName: 'nodejs'){
                    sh "npm install"
                }
            }
        }
    }
}
