pipeline {
    agent any
    environment {
        f_img = 'frontend_image'
        b_img = 'backend_image'
        net_name = 'docker_net'
        f_cont = 'frontend_container'
        b_cont = 'backend_container'
        db_name = 'mongodb'
    }
    stages {

        stage ('SCM Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/SyedShakirX/3-Tier-MERN-Jenkins-Docker.git'
            }
        }

        stage ('Build Frontend'){
            steps{
                echo "Building Frontend"
                sh 'docker build -t ${f_img} ./mern/frontend'
            }
        }

        stage ('Build Backend'){
            steps{
                echo "Building Backend"
                sh 'docker build -t ${b_img} ./mern/backend'
            }
        }

        stage ('Pull Database'){
            steps{
                echo "Pulling Mongo Database"
                sh 'docker pull mongo'
            }
        }

        stage ('Creating Network'){
            steps{
                echo "Creating Docker Network"
                sh 'docker network create ${net_name}'
            }
        }

        stage ('Run The Frontend'){
            steps{
                echo "Starting Frontend..."
                sh 'docker run -d -p 5173:5173 --network=${net_name} --name=${f_cont} ${f_img}'
            }
        }

        stage ('Run The Database'){
            steps{
                echo "Starting Mongo Data Base"
                sh 'docker run -d -p 27017:27017 --network=${net_name} --name=${db_name} mongo'
            }
        }

        stage ('Run The Backend'){
            steps{
                echo "Starting The Backend"
                sh 'docker run -d -p 5050:5050 --network=${net_name} --name=${b_cont} ${b_img}'
            }
        }

    }
}
