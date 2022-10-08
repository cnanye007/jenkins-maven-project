pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '/opt/apache-maven-3.8.6/bin/mvn -f hello-app/pom.xml -B -DskipTests clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts....."
                    archiveArtifacts artifacts: '**/*.jar'
                }
            }
        }
        stage('Test') {
            steps {
                sh '/opt/apache-maven-3.8.6/bin/mvn -f hello-app/pom.xml test'
            }
            post {
                always {
                    junit 'hello-app/target/surefire-reports/*.xml'
                    step( [ $class: 'JacocoPublisher' ] )
                }
            }
        }
    }
}
