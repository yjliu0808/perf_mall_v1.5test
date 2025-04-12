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
        stage('验证拉取') {
            steps {
                echo "✅ 自动构建成功，代码仓库已正确拉取."
                echo "当前 JMeter 脚本文件：${SCRIPT_NAME}"
            }
        }
    }

    post {
        always {
            echo "✅ 构建测试流程完成"
        }
    }
}
