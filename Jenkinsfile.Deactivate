pipeline {

  agent {
    node {
      label 'agent'
    }
  }

  options {
    // Default buildDiscarder configuration, Declarative Pipeline Syntax
    buildDiscarder logRotator(artifactNumToKeepStr: '1', numToKeepStr: '1')
    // Filter buildDiscarder detail definitions, wanted similar Declarative Pipeline Syntax
    // I think for this buildDiscarder needs more than one logRotator
    // buildDiscarder logRotator(filter: 'Production', daysToKeepStr: 'UMLIMITED')
    // buildDiscarder logRotator(filter: 'Quality Assurance', daysToKeepStr: '30')
  }

  stages {

    stage ("Build Sources") {
      steps {
        echo 'Do all the build stuff, no Build Discarder filter, so use the default here'
      }
    }

    stage ("Ask Deploy Quality Assurance") {
      when {
        branch 'master'
        beforeAgent true
      }
      steps {
        input message: 'Do you really want to deploy to Quality Assurance?'
      }
    }
        
    stage ("Deploy to Quality Assurance") {
      when {
        branch 'master' 
        beforeAgent true
      }
      steps {
        echo 'Do all the deployment to Quality Assurance stuff, after that set the Quality Assurance filter for the build'
        // buildDiscarderFilter (filter: 'Quality Assurance')
      }
    }

    stage ("Ask Deploy Production") {
      when {
        branch 'master'
        beforeAgent true
      }
      steps {
        input message: 'Do you really want to deploy to Production?'
      }
    }
        
    stage ("Deploy to Production") {
      when {
        branch 'master' 
        beforeAgent true
      }
      steps {
        echo 'Do all the deployment toProduction stuff, after that set the Production for the build filter'
        // buildDiscarderFilter (filter: 'Production')
      }
    }

  }

}
