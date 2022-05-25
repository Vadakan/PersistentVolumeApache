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


# use 'persistent volume claim' in our pod definition like below to access the persistent volume


![image](https://user-images.githubusercontent.com/80065996/170307641-c687e68b-5baf-4651-bee6-ce01a1dea2b1.png)


![image](https://user-images.githubusercontent.com/80065996/170307907-406f3831-99a9-4397-a7af-9bc84bd7acf0.png)


# step by step how "persistent volume' is used.


![image](https://user-images.githubusercontent.com/80065996/170309197-9d71ddb4-f656-413b-8ea7-94f984be7a25.png)


# "persistent volume claim" should be present in same "namespace" as of the pod which it is using. (or else pod cannot access it)
# "persistent volume" are not namespaced but "persistent volume claim" are namespaced.


![image](https://user-images.githubusercontent.com/80065996/170309553-8251366a-b544-409c-9250-44ecb88b70fd.png)


![image](https://user-images.githubusercontent.com/80065996/170312415-c999c07a-ed05-4426-89b3-a88f41bad9f6.png)


# volume is first mounted into the pod and then to the container


![image](https://user-images.githubusercontent.com/80065996/170312829-1070e139-4c89-464c-ada8-8264c0e90754.png)


![image](https://user-images.githubusercontent.com/80065996/170313767-542cbc98-214e-4957-820d-7804b5c282c7.png)


# why so many abstractions ?


![image](https://user-images.githubusercontent.com/80065996/170314108-b2373e5c-6a8e-4926-9015-85a69593943f.png)


# Developers needs not to worry about storage part. they can concentrate only on deploying the applications. developers will be good as long as their
# storage are safe.


![image](https://user-images.githubusercontent.com/80065996/170322642-042f01b6-7ed2-42ba-99e3-224cd0a688de.png)


# configmap and secret as volumes:


![image](https://user-images.githubusercontent.com/80065996/170323686-cf47f6e9-1b74-44eb-85fe-566262cc5b64.png)


![image](https://user-images.githubusercontent.com/80065996/170323862-8238b90d-d53b-49c6-a325-7f533ccd31ee.png)


![image](https://user-images.githubusercontent.com/80065996/170324070-ab9d8b4d-ce7b-49e2-922c-42bf856eb4fe.png)


![image](https://user-images.githubusercontent.com/80065996/170324410-53532708-d517-4a43-8eff-8dcfdf4ff8fc.png)


![image](https://user-images.githubusercontent.com/80065996/170324525-c302a1a5-381a-4569-aa5a-dd6d8567fcb7.png)


![image](https://user-images.githubusercontent.com/80065996/170324728-7a0b4354-45bc-4437-aefe-ae1a12637f5e.png)


![image](https://user-images.githubusercontent.com/80065996/170325113-44fe4519-be1a-49f6-9c56-13e37376b217.png)


# same pod can use different 'volume types'


![image](https://user-images.githubusercontent.com/80065996/170325513-ea235cb9-b4d1-4ab4-942e-60566ccaf149.png)


![image](https://user-images.githubusercontent.com/80065996/170325645-73e1bd15-32ae-4f05-b4ce-7d1a71456054.png)


![image](https://user-images.githubusercontent.com/80065996/170325830-aef08116-4e0b-4e5e-b15e-8d082524a9f6.png)


![image](https://user-images.githubusercontent.com/80065996/170325998-0e99ce21-d26b-4254-99da-11c418a3f314.png)


# storage class
# kuberneted admin creates 'storage class' & 'Persistent Volume'. Developers create 'persistent volume claim' and use it along with their pod configuration. 'persistent volume claim' will use 'persistent volume' to bind and store their data.


![image](https://user-images.githubusercontent.com/80065996/170326258-a979c092-0dd1-4d02-8cf4-662e372d3f86.png)


# lets take hunderds of application need their 'persistent volume' for their deployment. so everyone will go and request 'kubernetes admin' to create 
# 'persistent volume' and then he created many 'persistent volume' for many applications.
# Creation of 'persistent volume' is a manual job for kubernetes admin and it is really time consuming for creating 'persistent volumes' for many applications.


![image](https://user-images.githubusercontent.com/80065996/170326830-61ef3634-3cf8-4198-b2ac-21311716e1aa.png)


# to make admin's life easier in this manual job, there is a another component in kubernetes called 'storage class'


![image](https://user-images.githubusercontent.com/80065996/170327186-f7e79346-f7c1-4760-b4e5-e89f8a82eed8.png)


![image](https://user-images.githubusercontent.com/80065996/170327261-c7970210-33c8-4875-a5ad-ab838b7d1336.png)


# 'Storage class' creates 'persistent volume' dynamically whenever 'persistent volume claim' claims it.


![image](https://user-images.githubusercontent.com/80065996/170327392-1cc80663-2255-47d8-ad8b-12d9ba7c5af7.png)


# storage class yaml file


![image](https://user-images.githubusercontent.com/80065996/170327915-a299e0a4-79d2-49ba-ba6f-26b978a928c2.png)


# 'provisioner' fields in yaml tells use what kind of 'persistent volume' needs to be created whenever 'persistent volume claim' claims this 'storage class'


![image](https://user-images.githubusercontent.com/80065996/170328253-35a1c7a7-b2ab-4932-8d40-b9ec8d63dd58.png)

# we have tell 'storage class' yaml file on what kind of 'persistent volume' needs to be created from basic storage types which kubernetes supports. and also
# we have to mention the 'storage size' as well.


![image](https://user-images.githubusercontent.com/80065996/170328351-8f80f68e-4220-4a55-8081-9fea9083ea00.png)


![image](https://user-images.githubusercontent.com/80065996/170328535-90f6e077-ac6b-49ca-9edf-d0c22fc47d27.png)


# how to use this 'storage class' in our 'pod' configuration
# we have to mention the name of 'storage class' in 'persistent volume claim' config yaml file
# 'persistent volume claim' name will be mentioned in 'pod' configuration. 
# so pod will request 'persistent volume claim' and in turn 'persistent volume claim' calls the 'storage class' so that 'storage class' will automatically create the 'persistent volume' for us which in turns binds the 'persistent volume' with our 'persistent volume claim'


![image](https://user-images.githubusercontent.com/80065996/170328642-c1680d9c-c0ff-45b2-946f-b65d6cd94e5a.png)


![image](https://user-images.githubusercontent.com/80065996/170328702-34dd6bf3-22e9-4229-a743-6080d1ee29b3.png)


![image](https://user-images.githubusercontent.com/80065996/170328791-13b5dfbb-5918-4010-bf42-33026be5ecd6.png)



