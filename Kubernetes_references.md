
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
         
         
       
 
