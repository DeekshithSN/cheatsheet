## Docker save

- docker save image_name:tag > file_name.tar
- docker save --output busybox.tar busybox 
- docker save -o fedora-all.tar fedora 

## Docker load

- docker load -i file_name.tar

## copy the files to running container 

- docker cp source_path containerid:destination_path

        docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-
        docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH
        
## building docker images 

- docker build .
 To build Dockerfile present in current directory and . means send current directory as build context 
 
- docker build -f test.txt .
 Assume your project has a requirment that name of the docker file should be test.txt then above is the command to build the file
 
