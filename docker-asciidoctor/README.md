# Instructions

Parent document containing the instrcutions to configure github and travis-ci : http://mgreau.com/posts/2016/03/28/asciidoc-to-gh-pages-with-travis-ci-docker-asciidoctor.html
As the dockerfile of the existing asciidoctor image contains errors, a new image has been defined here.

Open a terminal within this project and execute these commands to clone the project containing the lab :

    git clone https://github.com/gastaldi/lab-forge-swarm-keycloak.git

Create the Docker container

    docker-machine create --driver=virtualbox asciidoctor
    docker-machine env asciidoctor
    eval $(docker-machine env asciidoctor)

Build it 

    docker build -t cmoulliard/docker-asciidoctor .
    
 Push the newly image to Docker.io 
    
    docker push cmoulliard/docker-asciidoctor

Generate the HTML & PDF

. Locally

    docker run -it -v /Users/chmoulli/MyProjects/asciidoctor-build/lab-forge-swarm-keycloak:/documents/ cmoulliard/docker-asciidoctor
    
and then generate the documents
    
    asciidoctor README.adoc
    asciidoctor-pdf README.adoc
    
 using a different style
    
    asciidoctor -a stylesheet=$STYLES/foundation.css README.adoc -o README-foundation.html
    
. Travis
    
    