pipeline {
 agent any
 stages {
       stage("Build") {
            steps {
                sh 'php --version'
                sh 'composer --version'
                sh 'cp .env.example .env'
                sh 'php artisan key:generate'
            }
        }
        stage("Unit test") {
            steps {
                sh 'php ./vendor/bin/phpunit tests/Feature/RouteTest.php'
            }
        }
        stage("Code coverage") {
            steps {
                sh "vendor/bin/phpunit tests/Feature/RouteTest.php --coverage-html 'reports/coverage'"
            }
        }
        /*stage("Static code analysis larastan") {
            steps {
                sh "vendor/bin/phpstan analyse --memory-limit=2G"
            }
        }
        stage("Static code analysis phpcs") {
            steps {
                sh "vendor/bin/phpcs"
            }
        }
      /*  stage("Deploy to staging") {
            steps {
                sh "docker cp jenkins:/var/jenkins_home/workspace/CloudWineBackend /var/www/"
            }
        }*/
  }
}
