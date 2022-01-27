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
      stage("Docker build") {
            steps {
                sh "docker rmi r0710377/laravel8cd"
                sh "docker build -t r0710377/laravel8cd --no-cache ."
            }
        }
        stage("Docker push") {
            environment {
                DOCKER_USERNAME = credentials("sethpeeters")
                DOCKER_PASSWORD = credentials("Kaka_1234")
            }
            steps {
                sh "docker login --username ${DOCKER_USERNAME} --password ${DOCKER_PASSWORD}"
                sh "docker push r0710377/laravel8cd"
            }
        }
        stage("Deploy to staging") {
            steps {
                sh "docker run -d --rm -p 80:80 --name laravel8cd r0710377/laravel8cd"
            }
        }
  }
}
