# Practice6
Проектирование и развертывание веб-решений в эко-системе Python - задание 6

## Stage 1: The Basics

### 1.1 Your First Linux Containers:
docker container run hello-world
docker image pull alpine
docker container run alpine ls -l
docker container run alpine echo "hello from alpine"
docker container run alpine /bin/sh
docker container run -it alpine /bin/sh
docker container ls -a
![image](https://github.com/user-attachments/assets/f42c2639-bb0e-411c-b071-5a2fec3fc811)
docker container run -it alpine /bin/ash
![image](https://github.com/user-attachments/assets/22fc3d52-d969-426f-b8ce-7cad4815355f)
docker container exec sleepy_borg ls
![image](https://github.com/user-attachments/assets/5ce9fe44-d9df-4f95-b704-a4069bac1a26)

### 1.2 Customizing Docker Images:
docker container run -ti ubuntu bash
apt-get update
apt-get install -y figlet
figlet "hello docker"
![image](https://github.com/user-attachments/assets/638f077d-c634-4ee3-a5ac-6b7a3d5f7cc9)
exit
docker container ls -a
![image](https://github.com/user-attachments/assets/6dc8bb3f-bb07-4ee5-a994-e14c15ff7f94)
docker container diff 9ea74841d09c
docker container commit 9ea74841d09c
![image](https://github.com/user-attachments/assets/a09831f6-7765-4980-845b-d54f6a5d516d)
docker image ls
![image](https://github.com/user-attachments/assets/36abdfd9-4b83-43f6-9a23-eaff4c899ad6)
docker image tag b7a085fe14f7 ourfiglet 
docker image ls
![image](https://github.com/user-attachments/assets/a21bfbe2-f3f1-45da-8f85-ed4c82e46797)
docker container run ourfiglet figlet "hello"
![image](https://github.com/user-attachments/assets/d4f2dc90-ed05-4881-b6c6-e62db32d4d72)

![image](https://github.com/user-attachments/assets/647291d9-a486-4e25-aecf-669d510f20a4)
![image](https://github.com/user-attachments/assets/a296e6d0-8751-4794-ae9c-bf2a8f9c5efc)
docker image build -t hello:v0.1 .
docker container run hello:v0.1
![image](https://github.com/user-attachments/assets/983f19d6-0699-46d1-b509-80daaa4e0ecd)
docker image history 6260342bfa5e
![image](https://github.com/user-attachments/assets/dfda466d-290c-46be-8d83-229415a85de9)
![image](https://github.com/user-attachments/assets/abff4daf-052a-4722-a21d-8518008ad632)
docker image build -t hello:v0.2 .
![image](https://github.com/user-attachments/assets/3fad9bed-34fa-4f66-9ea2-eb259ee94286)
![image](https://github.com/user-attachments/assets/f7f99199-3bef-4b80-9410-d82cd0f39870)
docker image pull alpine
docker image inspect alpine
![image](https://github.com/user-attachments/assets/9fc6ae8c-0d9d-4b59-b8d7-f743ad1e3919)
![image](https://github.com/user-attachments/assets/27c44d73-5255-4646-a58e-f9fe47973125)
![image](https://github.com/user-attachments/assets/1860aa83-8471-4a82-ad31-def22cb65204)
docker image inspect --format "{{ json .RootFS.Layers }}" alpine
![image](https://github.com/user-attachments/assets/219908d3-e0a2-49f7-8290-4f00056053fb)
docker image inspect --format "{{ json .RootFS.Layers }}" 0e38039f22b1
![image](https://github.com/user-attachments/assets/1e9988b1-a3bd-4fa6-8969-941467e70716)

### 1.3 Deploy and Managing Multiple Containers:
docker swarm init --advertise-addr $(hostname -i)
![image](https://github.com/user-attachments/assets/082c203b-fce9-4f57-85ff-c78108bb6319)
docker swarm join --token SWMTKN-1-2x110nj9r19jmbxyyeo76fvjxy1h429bswymgcfunx3t74jy28-1j1s7dawiespjtdj72r4mxnjo 192.168.0.8:2377
![image](https://github.com/user-attachments/assets/13fb0888-035e-4cd0-93e2-188435683bf8)
