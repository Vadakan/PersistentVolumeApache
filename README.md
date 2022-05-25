# PersistentVolumeApache


![image](https://user-images.githubusercontent.com/80065996/170291212-a286b31d-e7e7-4696-a8ee-f85e94ecd684.png)


# Need for Persistent Volumes:
# when we have database pod and if it crashed all the data will be lost. instead we have to create a persistent volume to store the data and when the destroyed pod
# again comes up, we can have data present in persistent volumes and it will be taken by the pod.


![image](https://user-images.githubusercontent.com/80065996/170291359-e589ec37-d9fe-4e22-a4da-79908d345eb7.png)


![image](https://user-images.githubusercontent.com/80065996/170291922-495b284c-26a7-4dbc-8728-827e052e0b7e.png)


![image](https://user-images.githubusercontent.com/80065996/170292078-7b000e2c-762a-4520-acba-8bb841850b74.png)


# we dont know on which node our destroyed pod starts up. so our persistent volume should be common to the entire cluster so that pod started in any nodes can access this and get the data.


![image](https://user-images.githubusercontent.com/80065996/170292362-70891382-5c0f-42c7-a7f2-244ecbbd254f.png)


![image](https://user-images.githubusercontent.com/80065996/170292474-823d8e63-41bf-47a2-86bd-d7a3234c7484.png)


![image](https://user-images.githubusercontent.com/80065996/170292545-a3a297c9-d0af-4989-8abd-5ebf50cd7e24.png)


![image](https://user-images.githubusercontent.com/80065996/170292669-159c94a3-e484-43de-b8d0-de31f0b87af9.png)


# Another use case of persistent volumes other than database,
# we can use to store logs, session data by creating volume as a directory


![image](https://user-images.githubusercontent.com/80065996/170292927-0f89ded0-2643-4cb2-8247-3f043c97206d.png)


# think of persistent volume as cluster resource like RAM,CPU


![image](https://user-images.githubusercontent.com/80065996/170293297-53e5e4af-8199-4112-b9a5-91f65a020a39.png)


![image](https://user-images.githubusercontent.com/80065996/170293515-f83d5e22-eb13-4192-9682-1c5ea2517eb4.png)


# type of persistent volumes:re
# we can create 1) local storage on nodes as a directory 2) network file server (nfs server)  3) cloud storage in AWS,GCP,AZURE


![image](https://user-images.githubusercontent.com/80065996/170293675-9fd170b2-3746-4f76-81af-4873fcbc0351.png)


# We have to first decide what type of storage we need,


![image](https://user-images.githubusercontent.com/80065996/170296344-f3998129-19cb-4aba-acc5-92bd2ceec10a.png)


# Think of 'persistent volume' is like external plugin to our cluster


![image](https://user-images.githubusercontent.com/80065996/170296559-3958130e-e9e0-48a4-bc58-be4f5639ddad.png)


# we can make some application in cluster used NFS, some application uses cloud storage and some can use local storage


![image](https://user-images.githubusercontent.com/80065996/170299408-d8505e5d-230f-4244-bbd7-c87c4359190f.png)


# NFS server


![image](https://user-images.githubusercontent.com/80065996/170299655-37a2a501-c341-4f1e-b41d-bc8739fcf571.png)


# google cloud


![image](https://user-images.githubusercontent.com/80065996/170300060-e3bc3df0-f25f-4a78-bfcb-e079fe190b7e.png)


# local storage on the node


![image](https://user-images.githubusercontent.com/80065996/170300241-4ab435f1-33cf-46b4-a4bb-623f5ec78e0f.png)


# LIST OF storage backend supported by kubernetes


![image](https://user-images.githubusercontent.com/80065996/170300548-f89f9d43-db8a-418d-af23-9ca81ed0c0a7.png)


# persistent volumes are not namespaced


![image](https://user-images.githubusercontent.com/80065996/170301314-bdc6f26c-b2f9-4da6-a23a-26299f86b4f8.png)


![image](https://user-images.githubusercontent.com/80065996/170301384-76ccacf4-7795-446a-a9cf-8d9f7fd39782.png)


# local vs remote volume types


![image](https://user-images.githubusercontent.com/80065996/170301596-583ac087-3a19-41bb-b8ab-52584296296f.png)


![image](https://user-images.githubusercontent.com/80065996/170301890-b623da8e-f040-4803-8ae0-191e550551fa.png)


# for database purpose use case, always use "remote volumes" which can survive even cluster crash


# who creates persistent volume and when ? (note: this is "persistent volume" not "persistent volume claim")
# "persistent volume" is like CPU,memory which should be already present before in the cluster.
# Pod which needs this "persistent volume" will create the "persistent volume claim"


![image](https://user-images.githubusercontent.com/80065996/170302421-7f246259-1b00-4701-b273-8557e2320235.png)


![image](https://user-images.githubusercontent.com/80065996/170302748-60ed9c44-e927-4e2f-b3ea-4628588ae115.png)


# kubernetes admin - 1) set up cluster 2) create storage (nfs, cloud storage, local) from storage backend supported by kubernetes. 3) create "persistent volume" in the cluster based on "storage backends" supported.


![image](https://user-images.githubusercontent.com/80065996/170303336-8bf5b038-7513-4400-8bc3-04f6707552e1.png)


# now application team says what type of "persistent volume" they need.


![image](https://user-images.githubusercontent.com/80065996/170304548-9108dbef-1bf3-43b8-b530-2c4344e6c4fb.png)


# once kubernetes admin created "persistent volume" from storage backend supported by kubernetes on the cluster, development team need to create 
# the "persistent Volume Claim" and attach to that our pod so that pod will use the storage available in "persistent volume" present in cluster created by
# kubernetes administrator.


![image](https://user-images.githubusercontent.com/80065996/170305353-88f02fbc-cdd6-49d1-a396-7f0d49e7a91f.png)


![image](https://user-images.githubusercontent.com/80065996/170305561-5915ae76-243e-4d08-80f7-8a30343614f7.png)


# there will be multiple "persistent volume" of different types available in the cluster. whatever details mentioned in our "persistent volume claim" matched with "persistent volume" available in the cluster, it will be picked up by our pods. 
# 1) storage space 2) storage class 3) type of storage


![image](https://user-images.githubusercontent.com/80065996/170306586-cea6c68a-d420-436c-90aa-8367f01dda80.png)






