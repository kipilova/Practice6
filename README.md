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
docker node ls
![image](https://github.com/user-attachments/assets/09436ef3-24f5-4bc3-b459-c541b789951e)
git clone https://github.com/docker/example-voting-app
cd example-voting-app
![image](https://github.com/user-attachments/assets/43c9f547-de29-4dec-8f96-16cd31e1b1f1)
cat docker-stack.yml
![image](https://github.com/user-attachments/assets/a3e03f40-2deb-49cc-9c3c-801f03f41784)
docker stack deploy --compose-file=docker-stack.yml voting_stack
![image](https://github.com/user-attachments/assets/2365db2e-d78e-4d37-9aa7-286f0fc6c7dc)
docker stack ls
![image](https://github.com/user-attachments/assets/365b89e1-8838-4883-9868-eba9031b739a)
docker stack services voting_stack
![image](https://github.com/user-attachments/assets/a2696dc2-3b77-4f66-9494-b6c4114931a9)
docker service ps voting_stack_vote
![image](https://github.com/user-attachments/assets/8b858419-b284-49a4-8096-6a682220a875)
docker service scale voting_stack_vote=5
![image](https://github.com/user-attachments/assets/910a55b4-da59-43e3-93a4-6858c8df2d6c)

## Stage 2: Digging Deeper

### 2.1 Security Lab: Seccomp
git clone https://github.com/docker/labs
cd labs/security/seccomp
docker run --rm -it --cap-add ALL --security-opt apparmor=unconfined --security-opt seccomp=seccomp-profiles/deny.json alpine sh
![image](https://github.com/user-attachments/assets/e9c90119-6a06-4a3f-9911-8c592c74bbb9)
cat seccomp-profiles/deny.json
![image](https://github.com/user-attachments/assets/09b3e35d-c688-4195-9041-2955d7246c91)
docker run --rm -it --security-opt seccomp=unconfined debian:jessie sh
docker run -it alpine /bin/sh
apk add --update strace
![image](https://github.com/user-attachments/assets/2abe5c82-4900-4127-95e1-1e6c98ecd4b5)
strace -c -f -S name whoami 2>&1 1>/dev/null | tail -n +3 | head -n -2 | awk '{print $(NF)}'
![image](https://github.com/user-attachments/assets/a3766221-5cee-4e45-a89a-9a9c68f36085)
exit
docker run --rm -it --security-opt seccomp=./seccomp-profiles/default-no-chmod.json alpine sh
chmod 777 / -v
![image](https://github.com/user-attachments/assets/9b983c8f-38de-4cfb-8e1e-eb85c13cb9de)
exit
docker run --rm -it --security-opt seccomp=./seccomp-profiles/default.json alpine sh
chmod 777 / -v
![image](https://github.com/user-attachments/assets/382ff607-6505-40ee-9aea-aef04acc25ec)
exit
cat ./seccomp-profiles/default.json | grep chmod
![image](https://github.com/user-attachments/assets/81208888-54e6-4a69-a340-5592b3591661)
cat ./seccomp-profiles/default-no-chmod.json | grep chmod

### 2.2 Security Lab: Capabilities
docker run --rm -it alpine chown nobody /
docker run --rm -it --cap-drop ALL --cap-add CHOWN alpine chown nobody /
docker run --rm -it --cap-drop CHOWN alpine chown nobody /
![image](https://github.com/user-attachments/assets/ab71c0ce-5a4c-4627-b25a-babfe30309d7)
docker run --rm -it --cap-add chown -u nobody alpine chown nobody /
![image](https://github.com/user-attachments/assets/95ef6b17-4de4-46f6-bc37-3c7a226999a8)
docker run --rm -it alpine sh -c 'apk add -U libcap; capsh --print'
![image](https://github.com/user-attachments/assets/6ba0e8e3-9ff8-4a3f-83a0-165825095c52)
![image](https://github.com/user-attachments/assets/9414606a-1619-408e-9f41-c983986a3ca7)
docker run --rm -it alpine sh -c 'apk add -U libcap;capsh --help'
![image](https://github.com/user-attachments/assets/e9bae9b5-4317-4dce-978e-6b9bfa71eaf0)
![image](https://github.com/user-attachments/assets/f75ed6e7-6cb8-4c3d-a95b-e2f0525086fa)
![image](https://github.com/user-attachments/assets/b8c8936d-b134-4781-9046-3b0fcd457075)

### 2.3 Docker Networking Hands-on Lab
docker network
![image](https://github.com/user-attachments/assets/17fb6e78-7c0a-485f-a2f3-4cebf5d8062c)
docker network ls
![image](https://github.com/user-attachments/assets/929578da-629e-4a1c-afb9-12555cb07467)
docker network inspect bridge





















