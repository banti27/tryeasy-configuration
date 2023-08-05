mavenJob('tryeasy-AUG-1') {
    properties {
        githubProjectUrl('https://github.com/banti27/tryeasy.git/')
    }
    scm {
        git('https://github.com/banti27/tryeasy.git/', 'master')
    }
  	rootPOM('pom.xml')
    goals('clean install')
    postBuildSteps('SUCCESS') {
    }
    publishers {
        publishOverSsh {
            server('tryeasy_docker_host') {
                transferSet {
                    sourceFiles('**/recordkeeping-0.0.1-SNAPSHOT.jar')
                    removePrefix('target/')
                }
                transferSet {
                    sourceFiles('Dockerfile')
                    execCommand('''
								docker build -t tryeasy .
								docker container stop $(docker container ls -aq)
								docker run -d --name tryeasy_container -p 8081:8080 tryeasy
								''')
                }
            }
        }
    }
}