
# kubernetes 

## Pod
   ### pod is a object which encapsulates or groups one or more containers (such as Docker containers), with shared storage/network, and a specification for how to run the containers.
   
   below is the basic structure of pod 
   
      apiVersion: v1
      kind: Pod
      metadata:
        name: my-first-app
        labels:
          type: front-end
      spec:
        conatiners:
          - name: busybox
            image: busybox
   
 - command to list the pods 
 
       kubectl get pods
 
 - command to create a pod with image busybox ( it actually creates deployment ) 
   
       kubectl run my-pod --image=busybox
   
 - command to delete a particular pod 
   
       kubectl delete pod pod_name 
       
 - if you have created pod using kubectl run command but you want see configrations of pod, so to get yml out of pod use below command 
  
       kubectl get pod pod_name -o yaml > my_pod_file.yaml
       
 - if you want describe your pod
       
       kubectl describe pod pod_name 
       
 - if you want to login for running pod
  
       kubectl exec -it pod_name /bin/sh
       
 - if you want access logs of any container inside pod 
 
       kubectl logs pod_name -c conatiner_name_inside_pod   ( container name inside pod you will get it by kubectl describe pod command ) 
       
 - let's say you have created pod using kubectl run command and now you want to change small configuration of pod then you can use below command
 
         kubectl edit pod pod_name ( it will open a vi editor , so you can change and save it back then you no need apply 
         it back kubernetes will automatically updates the pod )
             
 - let's you have created pods in any other namespaces ( other than default ) , to list them use below command 
         
         kubectl get pods --namespace=dev   ( assuming namespace is dev ) 
         

## ReplicaSet
   ### replicaset is an kubernetes object which is used make your pod highly available and any point time it will make sure sepcified replicas are up and running 
   
   basic structure replicaset 
   
         apiVesrion: apps/v1
         kind: ReplicaSet
         metadata: 
           name: my-rs
           lables:
             type: front-end
         spec:
           template:
             metadata:
               name: my-pod
               lables: 
                 type: front-end
             spec: 
              containers:
                - name: nginx
                  image: nginx 
           replicas: 6
           selector:
             matchLables:
               type: front-end

 when you create replica set , it automatically creates pods 
 
 - to list replicaset
      
         kubectl get rs or kubectl get replicasets 
 
 - to list replicasets in other name space 
    
         kubectl get rs --namespace=dev ( assuming namespace is dev ) 
        
 - to delete replicaset 
   
         kubectl delete rs rs_name
         
 - lets say replica set has been created via kubectl run command , you want to see configuration file of it 
 
         kubectl get rs rs_name -o yaml > rs_sample.yaml
         
 - lets say you want to edit rs 
 
         kubectl edit rs rs_name ( it opens vi editor and do the changes , save it back it automatically applies it back )
         
        but one thing to keep in mind is lets you have created rs with image busybox777 and replicas 3
        it creates 3 pods with status failed , you will change rs and apply it back
        but even then pods will with old configuration, so here you have 2 options 
        1. delete all old pods and now while creating new pods it will take updated configurations
        2. delete rs and re-create it
        
 - to increase or decrease replica count without changing rs yaml config file use below command 
 
         kubectl scale rs rs_name --replicas=6
