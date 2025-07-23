pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Run Maven build and skip tests (remove -DskipTests if you want tests to run)
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                # Kill any existing running instance of your app (adjust jar name if needed)
                pkill -f jenkins-java-app-1.0-SNAPSHOT.jar || true
                
                # Run the jar in background, output logs to app.log
                nohup java -jar target/jenkins-java-app-1.0-SNAPSHOT.jar > app.log 2>&1 &
                '''
            }
        }
    }
}

