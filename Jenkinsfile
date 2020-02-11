pipeline {
  stage "Sonarqube"
                def scannerHome = tool 'sonarqube'
                def projectKey = ‘test123’
                
                withSonarQubeEnv('sonarqube') {
                    sh "command -v detect-secrets >/dev/null 2>&1 || { echo >&2 "installing detect-secrets "; pip install detect-secrets;}"
                    sh "detect-secrets scan --no-keyword-scan --exclude-files 'package-lock.json|tests/*|test/*' > .secret.baseline"
                    sh "curl https://raw.githubusercontent.com/xendit/xendit-secret-scanner/feature/sonar/script/detect-conv.py\?token\=AMOZE6GX436W3QJSI6J6PF26JHLIA -o detect-conv.py"
                    sh "python detect-conv.py .secret.baseline detect-secret.json"
                    sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=${projectKey} -Dsonar.externalIssuesReportPaths=detect-secret.json"
                }

 }
