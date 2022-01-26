pipeline {
    agent any
    stages {
        /*stage("Build") {
            environment {
                DB_HOST = credentials("robincraft007.ddns.net")
                DB_DATABASE = credentials("poject")
                DB_USERNAME = credentials("project_user")
                DB_PASSWORD = credentials("project_password")
            }
            steps {
                sh 'php --version'
                sh 'composer install'
                sh 'composer --version'
                sh 'cp .env.example .env'
                sh 'echo DB_HOST=${DB_HOST} >> .env'
                sh 'echo DB_USERNAME=${DB_USERNAME} >> .env'
                sh 'echo DB_DATABASE=${DB_DATABASE} >> .env'
                sh 'echo DB_PASSWORD=${DB_PASSWORD} >> .env'
                sh 'php artisan key:generate'
                sh 'cp .env .env.testing'
                sh 'php artisan migrate'
            }
        }*/
        stage("Unit test") {
            steps {
                sh 'phpunit -c hpunit.xml'
            }
        }
    }
}
