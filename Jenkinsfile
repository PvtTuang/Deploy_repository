pipeline {
    agent any

    stages {
        stage('Get Latest Link') {
            steps {
                script {
                    def link = sh(script: 'python3 get_latest_link.py', returnStdout: true).trim()

                    def webhook_url = 'http://10.80.26.23:8080/generic-webhook-trigger/invoke' 

                    def response = httpRequest(
                        contentType: 'APPLICATION_JSON',
                        httpMode: 'POST',
                        requestBody: toJson(data),
                        url: webhook_url
                    )

                    if (response.status == 200) {
                        echo 'ส่งข้อมูลสำเร็จ'
                    } else {
                        error 'เกิดข้อผิดพลาดในการส่งข้อมูล'
                    }
                }
            }
        }
    }
}
