## Docker save
Assume you have requirment that need to save your docker image as .tar file below are the commands for the same 
- docker save image_name:tag > file_name.tar
- docker save --output busybox.tar busybox 
- docker save -o fedora-all.tar fedora 

## Docker load
if you want load .tar file as docker image 
- docker load -i file_name.tar

## copy the files to running container 

copying the file to\from the running container 

- docker cp source_path containerid:destination_path

        docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-
        docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH
        
## building Dockerfile  

- docker build .  <br />
 To build Dockerfile present in current directory and . means send current directory as build context 
 
- docker build -f test.txt .  <br />
 Assume your project has a requirment that name of the docker file should be test.txt then above is the command to build the file
 
- docker build -t test:1.20.1 .  <br />
 If you want to give name to a image then we need to use -t option basically for creating a tag 
 
- docker build --no-cache .  <br />
         Assume you dont want to use intermediate layers which are there in build cache , then we need to use the above coammand  <br /> 
 this helps when we build dockerfile once in a while  <br />
          senario :- assume your dockerfile has RUN yum install git when you ran one year ago it installed git 2.17.1 but when you run this command again as this layer already exists it wont install the latest version.  <br />
        So if we use --no-cache it will try build also with new layer 
        
 - docker build . --build-arg a=5
 
                Dockerfile <br />
                
                from busybox
                run echo "test"
                ARG a
                run echo "$a"
   by using above command we will be able to send arguments as launch arguments 
   
- docker build --compress . <br />
  Assume your build context is in GB , if you want to compress and send to docker demon then we need to use above command.
   
   --force-rm		  --> Always remove intermediate containers <br />
   --quiet , -q		  --> Suppress the build output and print image ID on success <br />
   --rm	true	          --> Remove intermediate containers after a successful build <br />
