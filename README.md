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





