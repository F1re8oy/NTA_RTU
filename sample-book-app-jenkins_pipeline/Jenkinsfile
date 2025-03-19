pipeline {
     agent any
     triggers{ pollSCM('*/1 * * * *') }
 
 
     stages {
         stage('Build') {
             steps {
                 script{
                     build()
                 }
             }
         }
         stage('Deploy to DEV') {
             steps {
                 script{
                     deploy("DEV", 1010)
                 }
             }
         }
         stage('Tests on DEV') {
             steps {
                 script{
                     test("BOOKS", "DEV")
                 }
             }
         }
         stage('Deploy to STG') {
             steps {
                 script{
                     deploy("STG", 2020)
                 }
             }
         }
         stage('Tests on STG') {
             steps {
                 script{
                     test("BOOKS", "STG")
                 }
             }
         }
         stage('Deploy to PRD') {
             steps {
                 script{
                     deploy("PRD", 3030)
                 }
             }
         }
         stage('Tests on PRD') {
             steps {
                 script{
                     test("BOOKS", "PRD")
                 }
             }
         }
     }
 }
 
 // for windows: bat "npm.."
 // for linux/macos: sh "npm .."
 
 def build(){
     echo "Building of node application is starting.."
     sh "ls"
     sh "npm install"
     // sh "npm test"
 }
 
 def deploy(String environment, int port){
    echo "Deployment to ${environment} has started.."
    git branch: 'jenkins_pipeline', poll: false, url: 'https://github.com/mtararujs/sample-book-app.git'
    sh "pm2 delete \"books-${environment}\" || exit 0"
    sh "pm2 start -n \"books-${environment}\" index.js -- ${port}"
 }
 
 def test(String test_set, String environment){
     echo "Testing ${test_set} test set on ${environment} has started.."
     git branch: 'books_tests', poll: false, url: 'https://github.com/mtararujs/api-automation.git'
     sh "npm install"
     sh "npm run ${test_set} ${test_set}_${environment}"
 }
 
 
 // Būvējuma izveidi;
 // Būvējuma izvietošanu “DEV” vidē;
 // Testu izpildi “DEV” vidē;
 // Būvējuma izvietošanu “STG” vidē;
 // Testu izpildi “STG” vidē;
 // Būvējuma izvietošanu “PRD” vidē;
 // Testu izpildi “PRD” vidē;