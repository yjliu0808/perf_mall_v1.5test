pipeline {
    agent any

    environment {
        JMETER_HOME = "/athena/jmeter/apache-jmeter-5.5"
        SCRIPT_NAME = "perf_mall_v1.5test.jmx"
        PROJECT_NAME = "CUI_api_auto_mall_v1.5test"
        REPORT_DATE = new Date().format("yyyy_MM_dd", TimeZone.getTimeZone("Asia/Shanghai"))
        RESULT_DIR = "jmeter-results/${PROJECT_NAME}/report_${REPORT_DATE}"
        RESULT_FILE = "jmeter-results/${PROJECT_NAME}/result.jtl"
    }

    stages {
        stage('准备目录') {
            steps {
                script {
                    sh "mkdir -p jmeter-results/${PROJECT_NAME}"
                }
            }
        }

        stage('执行 JMeter 测试') {
            steps {
                script {
                    sh """
                        ${JMETER_HOME}/bin/jmeter -n \\
                        -t ${SCRIPT_NAME} \\
                        -l ${RESULT_FILE} \\
                        -e -o ${RESULT_DIR}
                    """
                }
            }
        }

        stage('归档 HTML 报告') {
            steps {
                archiveArtifacts artifacts: "${RESULT_DIR}/**", fingerprint: true
            }
        }
    }

    post {
        always {
            echo "✅ JMeter 压测完成，报告已生成于 ${RESULT_DIR}"
        }
    }
}
