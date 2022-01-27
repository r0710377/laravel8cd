pipeline {
 agent any
 stages {
       stage("Build") {
            environment {
                DB_CONNECTION = "mariadb"
                DB_HOST = credentials("robincraft007.ddns.net")
                DB_PORT = "53306"
                DB_DATABASE = credentials("project")
                DB_USERNAME = credentials("project_user")
                DB_PASSWORD = credentials("project_password")
            }
            steps {
                sh 'php --version'
                sh 'composer --version'
                sh 'cp .env.example .env'
                sh 'echo DB_CONNECTION=${DB_CONNECTION} >> .env'
                sh 'echo DB_HOST=${DB_HOST} >> .env'
                sh 'echo DB_PORT=${DB_PORT} >> .env'
                sh 'echo DB_USERNAME=${DB_USERNAME} >> .env'
                sh 'echo DB_DATABASE=${DB_DATABASE} >> .env'
                sh 'echo DB_PASSWORD=${DB_PASSWORD} >> .env'
                sh 'php artisan key:generate'
                sh 'cp .env .env.testing'
                sh 'php artisan migrate'
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
        stage("Static code analysis larastan") {
            steps {
                sh "vendor/bin/phpstan analyse --memory-limit=2G"
            }
        }
        stage("Static code analysis phpcs") {
            steps {
                sh "vendor/bin/phpcs"
            }
        }
  }
}
