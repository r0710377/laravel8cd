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
  }
}
