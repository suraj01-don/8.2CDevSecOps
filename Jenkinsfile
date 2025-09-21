pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/suraj01-don/8.2CDevSecOps.git'
      }
    }

    // Quick sanity: prove Jenkins sees Node & npm
    stage('Node tool versions') {
      steps {
        bat 'node -v'
        bat 'npm -v'
      }
    }

    // Install deps (ignore postinstall scripts to avoid native builds on Windows)
    stage('Install Dependencies') {
      steps {
        bat 'npm ci --no-audit --ignore-scripts || exit /b 0'
      }
    }

    stage('Run Tests') {
      steps {
        bat 'npm test || exit /b 0'     // continue even if tests fail
      }
    }

    stage('Generate Coverage Report') {
      steps {
        bat 'npm run coverage || exit /b 0'
      }
    }

    // The security report you need for the video
    stage('NPM Audit (Security Scan)') {
      steps {
        bat 'npm audit || exit /b 0'
      }
    }
  }
}
