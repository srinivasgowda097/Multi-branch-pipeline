node {
    stage 'Build'
        git url: 'https://github.com/jfrogdev/project-examples.git'

    stage 'Artifactory configuration'
        def server = Artifactory.newServer url: "http://localhost:8081/artifactory", username:"admin", password:"password"
        def artifactoryMaven = Artifactory.newMavenBuild()
        artifactoryMaven.tool = "M3" // Tool name from Jenkins configuration
        artifactoryMaven.deployer releaseRepo:'libs-release-local', snapshotRepo:'libs-snapshot-local', server: server
        artifactoryMaven.resolver releaseRepo:'libs-release', snapshotRepo:'libs-snapshot', server: server
        def buildInfo = Artifactory.newBuildInfo()

    stage 'Exec Maven'
        rtMaven.run pom: 'maven-example/pom.xml', goals: 'clean install', buildInfo: buildInfo

    stage 'Publish build info'
        server.publishBuildInfo buildInfo
}
