import jenkins.model.*
import hudson.model.*

def slackMessage
def slackChannel

pipeline {
    agent any
    stages {
        stage('Build Parameters') {
            steps {
                script{
                    properties([
                            parameters([
                                    string(
                                           echo "checking that this block should work"
//                                         defaultValue: 'v5.4.23',
//                                         description: 'Enter the app version for current release',
//                                         name: 'APP_VERSION',
//                                         trim: true
                                    )
                            ])
                    ])
                }
            }
        }
        stage('Code Freeze') {
            steps {
                echo "Created release branch for all branches"
                echo "Wait for code freeze"
                input 'Code Freeze : Please provide input whether we should Proceed or Abort'
                echo "Set access rights for release branch"
                echo "App version : 5.4.23"
                slackSend channel: '#Abhishek', color: 'good', message: "Code Freeze is done for the release v5.4.23"
            }
        }
        stage('Build android apk') {
            steps {
                echo "Building apk from release branch"
                input 'building apk : Please provide input whether we should Proceed or Abort'
                echo "Wait for build of an apk"
                echo "Archive apk"
                slackSend channel: '#bug_zilla', color: 'good', message: "Android .apk  is build for the release v5.4.23"
            }
        }
        stage('Backend Deployment') {
            steps {
                echo "Deploying all microservices on stage"
                echo "Wait for Backend Deployment"
                input 'Backend deployment : Please provide input whether we should Proceed or Abort'
                echo "Triggering job for deployment on stage"
                slackSend channel: '#Abhishek', color: 'good', message: "Backend Deployment is done for the release v5.4.23"
            }
        }
        stage('Testing on stage') {
            parallel {
                stage('Automated API Suite [Stage]') {
                    steps {
                        echo "Triggering Automated API Suite [Stage]"
                        echo "Wait for automation report"
                        input 'Automated API Suite [Stage] : Please provide input whether we should Proceed or Abort'
                        echo "Analyse report"
                        slackSend channel: '#Abhishek', color: 'good', message: "Automated API Suite [Stage] is Passed for the release v5.4.23"
                    }
                }

                stage('Automated Regression suite') {
                    steps {
                        echo "Trigger regression suite"
                        echo "Wait for automation report"
                        input 'Automation Suite : Please provide input whether we should Proceed or Abort'
                        echo "Analyse report"
                        slackSend channel: '#Abhishek', color: 'good', message: "Automated Regression suite is Passed for the release v5.4.23"
                    }
                }
                stage('Manual Exploratory testing') {
                    steps {
                        echo "Send mail/slack message to testers with build link"
                        echo "Wait for manual sign off"
                        input 'After completing manual exploratory testing, please provide input whether we should Proceed or Abort'
                        slackSend channel: '#Abhishek', color: 'good', message: "Manual Exploaratory testing is Completed v5.4.23"
                    }
                }
            }
        }
        stage('Testing on Web-stage') {
            parallel {
                stage('Web-automated Regression suite') {
                    steps {
                        echo "Trigger regression suite"
                        echo "Wait for web-automation report"
                        input 'Web automation Suite : Please provide input whether we should Proceed or Abort'
                        echo "Analyse report"
                        slackSend channel: '#Abhishek', color: 'good', message: "Web-automated Regression suite is Passed for the release"
                    }
                }
                stage('Manual Exploratory testing on web') {
                    steps {
                        echo "Send mail/slack message to testers with build link"
                        echo "Wait for manual sign off"
                        input 'After completing manual exploratory testing, please provide input whether we should Proceed or Abort'
                        slackSend channel: '#Abhishek', color: 'good', message: "Manual Exploaratory testing is Completed on stage web"
                    }
                }
                stage('Manual Exploratory testing on iOS') {
                    steps {
                        echo "Send mail/slack message to testers with build link"
                        echo "Wait for manual sign off"
                        input 'After completing manual exploratory testing, please provide input whether we should Proceed or Abort'
                        slackSend channel: '#Abhishek', color: 'good', message: "Manual Exploaratory testing is Completed on iOS"
                    }
                }
            }
        }
        stage('Verify open bugs on Stage') {
            steps {
                echo "Fail pipeline if critical bugs are open"
                echo "Wait for Open bugs"
                input 'Open Bugs : Please provide input whether we should Proceed or Abort'
                echo "Communicate open bugs to team"
                slackSend channel: '#Abhishek', color: 'good', message: "Verify open Bugs:- there is no open/blocker bug on common stage env for the release v5.4.23"
            }
        }
        stage('Sign off') {
            parallel {
                stage('QA sign off') {
                    steps {
                        echo "Wait for manual sign off from QA"
                        input 'QA sign off : Please provide input whether we should Proceed or Abort'
                        slackSend channel: '#Abhishek', color: 'good', message: "QA Signoff for the release v5.4.23 is done"
                    }
                }
                stage('Security sign off') {
                    steps {
                        echo "Wait for manual sign off from security"
                        input 'Security sign off : Please provide input whether we should Proceed or Abort'
                        slackSend channel: '#Abhishek', color: 'good', message: "Security Signoff for the release v5.4.23 is done"
                    }

                }
                stage('Design sign off') {
                    steps {
                        echo "Wait for manual sign off from design"
                        input 'Design sign off : Please provide input whether we should Proceed or Abort'
                        slackSend channel: '#Abhishek', color: 'good', message: "Design Signoff for the release v5.4.23 is done"
                    }
                }
            }
        }
        stage('Backend Deployment on Production')
                {
                    steps {
                        echo "Wait for Backend Deployment on Production"
                        input 'Back End Deployment on Prod: Please provide input whether we should Proceed or Abort'
                        echo "Deploy backend to production "
                        slackSend channel: '#Abhishek', color: 'good', message: "Backend Deployment on Prod is completed for app v5.4.23"
                    }
                }
        stage('Build release apk') {
            steps {
                echo "Building apk from release branch"
                echo "Wait for release apk"
                input 'Build Release apk : Please provide input whether we should Proceed or Abort'
                echo "Archive apk"
                slackSend channel: '#Abhishek', color: 'good', message: "release build v5.4.23 has been made and shared with the stakeholders"
            }
        }
        stage('Sanity on Prod')
                {
                    parallel {

                        stage('Automated API Suite [Production]') {
                            steps {
                                echo "Triggering Automated API Suite [Production]"
                                echo "Wait for automation report"
                                input 'Automated API Suite [Production] : Please provide input whether we should Proceed or Abort'
                                echo "Analyse report"
                                slackSend channel: '#Abhishek', color: 'good', message: "Automated API Suite [Production] is Passed for the release v5.4.23"
                            }
                        }

                        stage('Automated Sanity suite') {
                            steps {
                                echo "Trigger Sanity suite"
                                echo "Wait for automated sanity"
                                input 'Sanity Automation : Please provide input whether we should Proceed or Abort'
                                echo "Analyse report"
                                slackSend channel: '#Abhishek', color: 'good', message: "Automated sanity suite on Prod is Passed on App v5.4.23"
                            }
                        }
                        stage('Exploratory Sanity testing') {
                            steps {
                                echo "Send mail/slack message to testers with build link"
                                echo "Wait for manual sign off"
                                input 'After completing manual exploratory testing, please provide input whether we should Proceed or Abort'
                                slackSend channel: '#Abhishek', color: 'good', message: "Exploratory sanity testing on Prod is completed for v5.4.23"
                            }
                        }
                    }
                }
        stage('Verify open bugs on Prod') {
            steps {
                echo "Wait for open bugs on production"
                echo "Fail pipeline if critical bugs are open"
                input 'Verify Bugs : Please provide input whether we should Proceed or Abort'
                echo "Communicate open bugs to team"
               slackSend channel: '#Abhishek', color: 'good', message: "Verify open bugs:- there are no open/blocker bugs on prod for the release v5.4.23"
            }
        }
        stage('Upload apk to play store') {
            steps {
                echo "Wait to upload an apk"
                echo "Apk to play store"
                input 'Upload apk to playstore 5% rollout : Please provide input whether we should Proceed or Abort'
                slackSend channel: '#Abhishek', color: 'good', message: "Release build v5.4.23 is uplaoded on playstore with 5% rollout"
            }
        }
        stage('Release note update') {
            steps {
                echo "Wait for release note to be updated"
                input 'Release note update for the given release : Please provide input whether we should Proceed or Abort'
                slackSend channel: '#Abhishek', color: 'good', message: "Release note updated for the v5.4.23done"
            }
        }
    }
}