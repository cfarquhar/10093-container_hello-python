node {
    def app

    stage('Clone repository') {
        // Let's make sure we have the repository cloned to our workspace
        checkout scm
    }

    stage('Build image A') {
        // This builds the actual image; synonymous to docker build on the command line
        app = docker.build("tl_demo/image-a:${env.BUILD_ID}", "-f Dockerfile-A ./")
    }

    stage('Scan Image A and Publish to Jenkins') {
        try {
            prismaCloudScanImage ca: '', cert: '', dockerAddress: 'unix:///var/run/docker.sock', ignoreImageBuildTime: true, image: "tl_demo/image-A:${env.BUILD_ID}", key: '', logLevel: 'debug', podmanPath: '', project: '', resultsFile: 'prisma-cloud-scan-results-A.json'
        } finally {
            prismaCloudPublish resultsFilePattern: 'prisma-cloud-scan-results-A.json'
        }
    }

    stage('Build image B') {
        // This builds the actual image; synonymous to docker build on the command line
        app1 = docker.build("tl_demo/image-b:${env.BUILD_ID}", "-f Dockerfile-B ./")
    }

    stage('Scan Image B and Publish to Jenkins') {
        try {
            prismaCloudScanImage ca: '', cert: '', dockerAddress: 'unix:///var/run/docker.sock', ignoreImageBuildTime: true, image: "tl_demo/image-B:${env.BUILD_ID}", key: '', logLevel: 'debug', podmanPath: '', project: '', resultsFile: 'prisma-cloud-scan-results-B.json'
        } finally {
            prismaCloudPublish resultsFilePattern: 'prisma-cloud-scan-results-B.json'
        }
    }
}