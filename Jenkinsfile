#!/usr/bin/env groovy

pipeline {
    agent any
    options { timestamps() }
    
    stages {
        stage('Creare PV on k8s') {
            steps {
                sh "cd application/wordpress"
                sh "pwd"
                sh "sudo kubectl apply -f application/wordpress/pv-volume-wordpress.yaml"
                sh "sudo kubectl apply -f application/wordpress/pv-volume-mysql.yaml"
            }
        }
        stage('Release Build on k8s') {
            steps {
                sh "sudo kubectl apply -k application/wordpress/."
                sh "sleep 30"
            }
        }
        stage('Verify pods/service/pv/pvc on k8s') {
            steps {
                sh "sudo kubectl get pods"
                sh "sudo kubectl get pv"
                sh "sudo kubectl get pvc"
                sh "sudo kubectl get services wordpress"
            }
        }
    }
}
