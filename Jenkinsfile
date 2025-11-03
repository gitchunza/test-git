pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // 이 단계에서 Jenkins는 Git 저장소 전체를 워크스페이스로 가져옵니다.
                // YOUR_GIT_REPOSITORY_URL은 Jenkins Item 설정에서 정의되므로 생략합니다.
                git branch: 'main' // 자격 증명 ID를 사용하거나 생략
            }
        }

        stage('Deploy to Web Server') {
            steps {
                script {
                    // Jenkins 워크스페이스에서 Nginx의 배포 경로로 파일을 복사합니다.
                    // /var/jenkins_home/web_data는 호스트의 ~/web_data와 마운트된 경로입니다.
                    sh 'echo "Starting deployment..."'
                    sh 'cp -f index.html /var/jenkins_home/web_data/index.html'
                    sh 'echo "Deployment successful! Check http://211.188.61.53"'
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                // Nginx 컨테이너 내부 네트워크를 통해 배포 확인
                sh 'curl http://nginx/index.html | grep "Welcome"'
            }
        }
    }
}