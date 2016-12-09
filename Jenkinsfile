node {
    stage('Checkout') {
        checkout scm
    }
    stage('Test') {
        echo "Hallo"
        echo "aha"
    }
    stage('Test2') {
        echo "Leute"
    }
    stage('Maven') {
        docker.image('maven:3.3.3-jdk-8').inside {
            sh 'mvn -B clean install'
        }
    }
}
