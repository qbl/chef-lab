# Learn Chef Rally - Learning Notes

## 0. Intro

This repository is learning notes I write while learning about Chef from [Learn Chef Rally](https://learn.chef.io/). This note is mainly created so that I can learn the materials as if I'm about to teach them to someone else, just as suggested in [The Feynman Technique](https://collegeinfogeek.com/feynman-technique/). If you find this note is useful, most credits go to the folks at Learn Chef Rally.

### Requirements

There are several alternatives to run Chef.

#### Using Chef with Docker

1. Install Docker
2. Launch an Ubuntu Container

   First, create a new directory that will be our main working directory.   
     
   `mkdir learn-chef`  
   `cd learn-chef`

3. Pull a docker image with Ubuntu operating system installed.  
   
   `docker pull ubuntu`  
   
4. Once the image is ready, launch a container from that image.  

   `docker run -it -v $(pwd):/root/chef-repo -p 8100:80 ubuntu /bin/bash`

