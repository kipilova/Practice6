# Practice6
Проектирование и развертывание веб-решений в эко-системе Python - задание 6

# Getting Started Walk-through for IT Pros and System Administrators

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
![image](https://github.com/user-attachments/assets/f275163a-24e3-4245-a09b-81a3f6fc05d5)
![image](https://github.com/user-attachments/assets/2e393fa0-598b-4de7-b7c1-bf5d7b39cd95)
docker run -it --privileged --network host alpine /bin/sh
apk update
apk add bridge-utils
brctl show
![image](https://github.com/user-attachments/assets/b07df937-ff02-416b-b81f-e89af42a2f47)
ip a
![image](https://github.com/user-attachments/assets/9c0c5fce-774c-4bfb-ab7b-d150f41db95d)
docker run -dt ubuntu sleep infinity
docker ps
![image](https://github.com/user-attachments/assets/4dbb2666-5e14-4e4c-89a8-d9b6da42485b)
docker network inspect bridge
![image](https://github.com/user-attachments/assets/1528b2b1-514d-48df-b802-11d109bd9291)
docker run --name web1 -d -p 8080:80 nginx
docker ps
![image](https://github.com/user-attachments/assets/dff1057d-1a6f-4b46-bc85-dd082ce0517f)
curl 127.0.0.1:8080
![image](https://github.com/user-attachments/assets/ab3a93bd-c1e4-4ffe-9a44-a9cc5acb3af7)
![image](https://github.com/user-attachments/assets/24312e07-80a7-4af3-93cc-aaf38e94d191)
docker swarm init --advertise-addr $(hostname -i)
![image](https://github.com/user-attachments/assets/8aa32db1-90ce-499c-9a7a-5b2439bf6822)
docker swarm join --token SWMTKN-1-0lehhmzcxoovysiu8naaa8mpmytptgpm4llm2kglnc2gdxis68-d7boogipuoqa4aa1k3rcg87d4 192.168.0.27:2377
![image](https://github.com/user-attachments/assets/0b3fa857-d8c2-4dc2-a070-9e0e190d7625)
docker node ls
![image](https://github.com/user-attachments/assets/fa9bfcd3-a478-41ec-8a21-80f77f6087c5)
docker network create -d overlay overnet
![image](https://github.com/user-attachments/assets/5802bed7-65bb-49ad-822c-fa9dffd3b1e2)
docker network ls
![image](https://github.com/user-attachments/assets/bbe4f091-96fb-46dd-a6e6-29cffa82e554)
Docker network ls
![image](https://github.com/user-attachments/assets/c46ec07f-2f26-47ee-8b69-aa0b533c6be0)
docker network inspect overnet
![image](https://github.com/user-attachments/assets/40d8c8cb-f27a-4e8a-bc4c-b0e6b934e772)
docker service create --name myservice \
--network overnet \
--replicas 2 \
ubuntu sleep infinity
![image](https://github.com/user-attachments/assets/320d71ab-d28a-46bd-93ae-bf36362d572d)
docker service ls
![image](https://github.com/user-attachments/assets/2f248c29-3896-4ffe-b48a-f97064d653b7)
docker service ps myservice
![image](https://github.com/user-attachments/assets/7fe58a2f-6035-4011-bb94-86f78cb37613)
docker network ls
![image](https://github.com/user-attachments/assets/60677146-4afb-4d6e-9441-890b65f0b5f1)
docker network inspect overnet
![image](https://github.com/user-attachments/assets/65c6b829-db25-4172-a683-667c651bc6c4)
docker network inspect overnet
![image](https://github.com/user-attachments/assets/990ca352-cbed-4fd2-9c6c-11970d07f256)
docker ps
![image](https://github.com/user-attachments/assets/b1c407df-d685-41fc-ab10-ff2a43f6d26c)
docker exec -it d95d516b0581 /bin/bash
apt-get update && apt-get install -y iputils-ping
ping -c5 10.0.0.6
![image](https://github.com/user-attachments/assets/85b906bb-bb55-40bd-b2d7-b2b32ef76bfb)
cat /etc/resolv.conf
![image](https://github.com/user-attachments/assets/aa6fdd8f-3f82-4855-8adb-7e8c03fd5bba)
ping -c5 myservice
![image](https://github.com/user-attachments/assets/181aefb9-7536-4e8c-ba1d-e217a55c88cb)
docker swarm leave --force

### 2.4 Docker Orchestration Hands-on Lab
docker run -dt ubuntu sleep infinity
![image](https://github.com/user-attachments/assets/a3cf0230-4491-4c01-9e11-f3a43d5331bc)
docker ps
![image](https://github.com/user-attachments/assets/da18ad81-2a10-451e-82e5-7d6cf867bf20)
docker swarm init --advertise-addr $(hostname -i)
![image](https://github.com/user-attachments/assets/819376be-7b93-42dd-9171-c428c8c9f9cc)
docker swarm join --token SWMTKN-1-4ynei7av6hewtg5q3asmrq0p0dtu0uetr9l5mkv8scd5foi3pn-cnqu3ouewyrzjcwc13uk403ii 192.168.0.17:2377
![image](https://github.com/user-attachments/assets/5943db25-ee63-4464-bf6b-fe7f97f54cfa)
docker node ls
![image](https://github.com/user-attachments/assets/d7ef4c0a-7a27-438f-94a4-a66ea49d7f35)
docker service create --name sleep-app ubuntu sleep infinity
![image](https://github.com/user-attachments/assets/3d5f6938-d6cf-42e8-8548-98325312a95a)
docker service ls
![image](https://github.com/user-attachments/assets/1f6c8f5d-9eb9-4bdb-bb9b-1363fa353557)
docker service update --replicas 7 sleep-app
![image](https://github.com/user-attachments/assets/e9641317-6330-45c6-8da8-60a71b41770e)
docker service ps sleep-app
![image](https://github.com/user-attachments/assets/95a130a7-5299-42fd-9281-6283d56847c9)
docker service update --replicas 4 sleep-app
![image](https://github.com/user-attachments/assets/b0640632-fb1f-4f35-ad0a-e6d3dafe63d6)
docker service ps sleep-app
![image](https://github.com/user-attachments/assets/1963ab3b-9b0c-4ae5-a119-43c08ff9ba3b)
docker node ls
![image](https://github.com/user-attachments/assets/c2a61d09-c685-4e2b-8d48-b6311ecd74b0)
docker ps
![image](https://github.com/user-attachments/assets/fccfedee-17b5-4a24-beb8-d74918bff93e)
docker node update --availability drain ipwe7oaen46s0uj7jb3uhttcd
docker node ls
![image](https://github.com/user-attachments/assets/fd171aea-e4b8-4918-be92-4977af367a41)
docker ps
![image](https://github.com/user-attachments/assets/7df04e59-aef1-4237-b090-3dfcdeab000e)
docker service ps sleep-app
![image](https://github.com/user-attachments/assets/5148e188-385d-4644-854d-bb22c6ba2128)
docker service rm sleep-app
docker ps
![image](https://github.com/user-attachments/assets/f125d396-3e49-4d17-9df3-4829deffba86)
docker kill 06c092d5c0cc
docker swarm --force

## Stage 3: Moving to Production
Ссылки не работают
![image](https://github.com/user-attachments/assets/26dc4411-08d7-4de2-844f-63dcf0594613)

# Getting Started Walk-through for Developers

## Stage 1: The Basics

### 1.1 Docker for Beginners - Linux
git clone https://github.com/dockersamples/linux_tweet_app
docker container run alpine hostname
docker container ls --all
![image](https://github.com/user-attachments/assets/3b85e729-4715-4249-8a46-313d49847c5c)
docker container run --interactive --tty --rm ubuntu bash
ls /
![image](https://github.com/user-attachments/assets/90d4747c-8366-4ed5-9b9c-27f29ab2f400)
ps aux
![image](https://github.com/user-attachments/assets/d5e60fff-0ccb-431c-9a5b-00879ebd5271)
cat /etc/issue
![image](https://github.com/user-attachments/assets/5aee41ae-6461-494d-8b57-214c7ae962d4)
exit
cat /etc/issue
![image](https://github.com/user-attachments/assets/726e0a5c-ac13-4908-8be0-ffdd9f389c15)
docker container run \
 --detach \
 --name mydb \
 -e MYSQL_ROOT_PASSWORD=my-secret-pw \
 mysql:latest
 docker container ls
 ![image](https://github.com/user-attachments/assets/259700d2-5c35-4e31-8889-2d860bfe2126)
 docker container logs mydb
 ![image](https://github.com/user-attachments/assets/b8f351dc-164a-4364-9bf3-588fcb484ef4)
 docker container top mydb
 ![image](https://github.com/user-attachments/assets/7bcebdd4-957d-4bdf-90cd-235a714fe2ed)
 docker exec -it mydb \
 mysql --user=root --password=$MYSQL_ROOT_PASSWORD --version
 ![image](https://github.com/user-attachments/assets/a5f1c6e8-f1b2-4acf-beff-98122a826837)
 docker exec -it mydb sh
 mysql --user=root --password=$MYSQL_ROOT_PASSWORD --version
 ![image](https://github.com/user-attachments/assets/2bf07031-aa5f-4b2c-a9cc-c6a1b7fe10e2)
 exit
 cd linux_tweet_app
 cat Dockerfile
 ![image](https://github.com/user-attachments/assets/5aa3ca7a-1553-4797-9f3a-19306293f095)
 export DOCKERID=akipilova
 echo $DOCKERID
 ![image](https://github.com/user-attachments/assets/67316b8d-6381-4029-9de2-f22971a62327)
 docker image build --tag $DOCKERID/linux_tweet_app:1.0 .
 ![image](https://github.com/user-attachments/assets/a35548d5-a292-445d-936f-dccebc3fde24)
 docker container run \
 --detach \
 --publish 80:80 \
 --name linux_tweet_app \
 $DOCKERID/linux_tweet_app:1.0
 ![image](https://github.com/user-attachments/assets/ebc44108-fc8f-4bd4-a42a-3c3de2057672)
 docker container rm --force linux_tweet_app
 docker container run \
 --detach \
 --publish 80:80 \
 --name linux_tweet_app \
 --mount type=bind,source="$(pwd)",target=/usr/share/nginx/html \
 $DOCKERID/linux_tweet_app:1.0
 ![image](https://github.com/user-attachments/assets/ebf8ef0c-636e-428c-8a38-99b2b1a0527d)
 cp index-new.html index.html
 ![image](https://github.com/user-attachments/assets/a2b85d76-89cd-4cd9-8730-04935743cf95)
 docker rm --force linux_tweet_app
 docker container run \
 --detach \
 --publish 80:80 \
 --name linux_tweet_app \
 $DOCKERID/linux_tweet_app:1.0
 ![image](https://github.com/user-attachments/assets/92629aae-15b0-48f7-8b4a-dc5c912cba30)
 docker rm --force linux_tweet_app
 docker image build --tag $DOCKERID/linux_tweet_app:2.0 .
 ![image](https://github.com/user-attachments/assets/4ff213f5-e89b-4c50-a4c5-111395735b48)
 docker image ls
 ![image](https://github.com/user-attachments/assets/5505d43e-30c9-4690-be1c-0bb7c781aed9)
 docker container run \
 --detach \
 --publish 80:80 \
 --name linux_tweet_app \
 $DOCKERID/linux_tweet_app:2.0
 ![image](https://github.com/user-attachments/assets/bbe29e39-0034-4a9c-9990-b476e11f7297)
  docker container run \
 --detach \
 --publish 8080:80 \
 --name old_linux_tweet_app \
 $DOCKERID/linux_tweet_app:1.0
 ![image](https://github.com/user-attachments/assets/07c633a0-dbfa-4c35-ab1a-b4f1f123f6c7)
 docker image ls -f reference="$DOCKERID/*"
 ![image](https://github.com/user-attachments/assets/f28bc5a2-4302-4dc0-b234-8d473260d65d)
 docker login -u akipilova
 docker image push $DOCKERID/linux_tweet_app:1.0
 ![image](https://github.com/user-attachments/assets/2ff31226-47f9-4921-a9d2-6617e8dd38e6)
 docker image push $DOCKERID/linux_tweet_app:2.0
 ![image](https://github.com/user-attachments/assets/c77f1c4b-893d-4e84-9381-103290d8f2e1)
 ![image](https://github.com/user-attachments/assets/ad588eb1-dc38-445e-b99a-8d75d52492fa)

### 1.2 Application Containerization and Microservice Orchestration
git clone https://github.com/ibnesayeed/linkextractor.git
cd linkextractor
git checkout demo
git checkout step0
tree
![image](https://github.com/user-attachments/assets/f921bab8-c6df-4c9b-823d-ccbe0a9a3b33)
cat linkextractor.py
![image](https://github.com/user-attachments/assets/f2a04e00-bae0-4082-b9a7-6c72c62716c9)
./linkextractor.py http://example.com/
![image](https://github.com/user-attachments/assets/25e58906-6155-4f20-a757-9dc47eaa8a85)
![image](https://github.com/user-attachments/assets/8ffa3ea7-1a9b-4f94-bb38-71d1ec549799)
ls -l linkextractor.py
![image](https://github.com/user-attachments/assets/1b20eb85-9d39-4bd6-b958-384ce0ec8732)
python3 linkextractor.py
![image](https://github.com/user-attachments/assets/c4ac3bfb-bc74-4568-b410-d17e5e2ee70d)
python linkextractor.py
![image](https://github.com/user-attachments/assets/ef6dd1d0-ed83-47bd-aa9c-97e5d36c46bf)
git checkout step1
cat Dockerfile
![image](https://github.com/user-attachments/assets/7b996a04-85fd-4fe5-a7bd-f9c35e30702b)
docker image build -t linkextractor:step1 .
![image](https://github.com/user-attachments/assets/21b70fc7-9f70-4a1e-ae7d-49b060290dc9)
docker image ls
![image](https://github.com/user-attachments/assets/b7489bf9-5945-40ea-9352-0769b003c094)
docker container run -it --rm linkextractor:step1 http://example.com/
![image](https://github.com/user-attachments/assets/62385eef-92cd-4192-a15b-3d6c7863f2b9)
![image](https://github.com/user-attachments/assets/dd5e742b-89e5-44d4-820b-33e6607f9e6c)
docker build -t linkextractor:step1 .
![image](https://github.com/user-attachments/assets/0588d737-cafc-450c-abf5-ac62b6a4351e)
docker container run -it --rm linkextractor:step1 http://example.com/
![image](https://github.com/user-attachments/assets/3241fda8-0888-4e86-9ad4-e0d70e02b44a)
docker container run -it --rm linkextractor:step1 https://training.play-with-docker.com/
![image](https://github.com/user-attachments/assets/3c9af064-45bc-40ae-a032-ae20ee9984bc)
git checkout step2
docker image build -t linkextractor:step2 .
docker image ls
![image](https://github.com/user-attachments/assets/76c79921-ca0a-4ac2-afc2-4deefc409f73)
docker container run -it --rm linkextractor:step2 https://training.play-with-docker.com/
![image](https://github.com/user-attachments/assets/d64b7007-7ccf-4231-9e3b-afb556d1e446)
docker container run -it --rm linkextractor:step1 https://training.play-with-docker.com/
![image](https://github.com/user-attachments/assets/6e0e4ebd-63e6-4f04-b80d-a85916c5bb34)
git checkout step3
cat Dockerfile
![image](https://github.com/user-attachments/assets/9f66f320-8a68-4ae2-9385-8258ecddd2dc)
![image](https://github.com/user-attachments/assets/f499ac5b-c1ce-4175-a896-d8616735cd93)
docker image build -t linkextractor:step3 .
docker container run -d -p 5000:5000 --name=linkextractor linkextractor:step3
![image](https://github.com/user-attachments/assets/7d5aac7a-a3ca-4b9a-a372-667f954d05c3)
docker container ls
![image](https://github.com/user-attachments/assets/164b9fd4-ceaa-4fc7-86c1-503951708121)
curl -i http://localhost:5000/api/http://example.com/
![image](https://github.com/user-attachments/assets/e844ec8e-b878-490d-bd2e-2df250cfafab)
![image](https://github.com/user-attachments/assets/c8e2aff4-b56b-40e7-8613-7a5c443186af)
docker container rm -f linkextractor
git checkout step4
cat docker-compose.yml
![image](https://github.com/user-attachments/assets/f02e5a2e-2f74-4a7a-970c-f224d6441df7)
docker-compose up -d --build
![image](https://github.com/user-attachments/assets/26d89506-0024-4dd3-a65e-4711d67f3322)
docker container ls
![image](https://github.com/user-attachments/assets/f2f5b526-4940-4a16-955b-453985840074)
curl -i "http://localhost:5000/api/http://example.com/"
![image](https://github.com/user-attachments/assets/3567b377-58f5-41d4-bcd5-5540aa1bacf7)
Invoke-WebRequest -Uri "http://localhost:5000/api/http://example.com/"
![image](https://github.com/user-attachments/assets/6127a127-73f1-47a8-a868-85520a744846)
sed -i 's/Link Extractor/Super Link Extractor/g' www/index.php
git reset --hard
docker-compose down
git checkout step5
![image](https://github.com/user-attachments/assets/faeff643-1af0-44f1-b899-c4e4c4548938)
![image](https://github.com/user-attachments/assets/41ff592a-dd9e-453a-a6b7-5a165eaabfe5)
![image](https://github.com/user-attachments/assets/d74766a3-7bdb-4432-99de-fd715ae20fd4)
docker-compose up -d --build
![image](https://github.com/user-attachments/assets/a67dcc73-a6cf-413a-a12d-2b3e28867e16)
docker-compose exec redis redis-cli monitor
sed -i 's/Link Extractor/Super Link Extractor/g' www/index.php
git reset --hard
docker-compose down
git checkout step6
![image](https://github.com/user-attachments/assets/06197d43-91c8-44f0-b8da-fd5493912c6f)
![image](https://github.com/user-attachments/assets/0a2a1291-2d59-493f-be62-993146625423)
![image](https://github.com/user-attachments/assets/1c986035-b5a3-4291-9489-2c5731c46e0c)
docker-compose up -d --build
![image](https://github.com/user-attachments/assets/7bac7687-a132-4e6f-a008-ea7a2a7426f4)
Invoke-WebRequest -Uri "http://localhost:4567/api/http://example.com/"
![image](https://github.com/user-attachments/assets/17cfff3f-3b3e-4b86-8cc0-83d1c800ff6f)
tail -f logs/extraction.log
docker-compose down
cat logs/extraction.log
![image](https://github.com/user-attachments/assets/aadd4ec2-feac-4a3c-bff0-49f5d125f187)

### 1.3 Deploying a Multi-Service App in Docker Swarm Mode
docker swarm init --advertise-addr $(hostname -i)
![image](https://github.com/user-attachments/assets/67d65d34-fcb1-48ab-8f8a-92ee13471545)
docker node ls
![image](https://github.com/user-attachments/assets/3bfd02ae-3736-4088-acad-808eae0bc69d)
git clone https://github.com/docker/example-voting-app
cd example-voting-app
![image](https://github.com/user-attachments/assets/5cde70ac-fc46-48f2-9b21-9572012336ae)
docker stack deploy --compose-file=docker-stack.yml voting_stack
![image](https://github.com/user-attachments/assets/8f913a55-8fab-41b5-a830-91f9d76f6038)
docker stack ls
![image](https://github.com/user-attachments/assets/a3a69284-d1fe-4695-afb4-e61aa34e47e4)
docker stack services voting_stack
![image](https://github.com/user-attachments/assets/f3dd649a-09dc-4b58-98d1-c75c096f0503)
docker service ps voting_stack_vote
![image](https://github.com/user-attachments/assets/8e6e6d09-4d19-4bb7-8e9d-b9e26cb1d470)

## Stage 2: Digging Deeper

### 2.1 Java Development: Eclipse
![image](https://github.com/user-attachments/assets/7cdd2097-3c64-4fdd-ba51-0aebd80ff19f)
![image](https://github.com/user-attachments/assets/1b6abfad-00a3-4be4-bb40-ac84243c89bf)
![image](https://github.com/user-attachments/assets/e983b800-9792-488b-972f-ec158f764f45)
git clone https://github.com/docker/labs
cd labs/developer-tools/java-debugging
![image](https://github.com/user-attachments/assets/66f33d6b-001f-49e2-a378-6443fe6d5b8e)
![image](https://github.com/user-attachments/assets/a846ddbe-2ad9-4891-8cc0-24fcc0231164)
![image](https://github.com/user-attachments/assets/52bec19a-4233-41e0-a484-3851cd8aeae2)
![image](https://github.com/user-attachments/assets/1bc06b8e-8153-448e-9de3-b051774a8f85)
![image](https://github.com/user-attachments/assets/28868f24-b48f-48ff-b677-f1cb9ba69817)
docker-compose up
![image](https://github.com/user-attachments/assets/d346b811-9919-4632-84bc-5165d527b199)







### 2.4 Live Debugging Node.js with Docker and Visual Studio Code
![image](https://github.com/user-attachments/assets/462c88d8-b37f-431a-a70b-c05bef362666)
![image](https://github.com/user-attachments/assets/7d6e1552-9a25-4894-b117-0e8c3bb53cad)
![image](https://github.com/user-attachments/assets/4d10b443-b7a8-4905-8031-7c702b370df0)
![image](https://github.com/user-attachments/assets/8f383116-2928-4f2b-861d-8931bff55318)
![image](https://github.com/user-attachments/assets/77d4d916-51a6-4609-8d6f-a2526510ab60)
![image](https://github.com/user-attachments/assets/be331673-a3c8-44ea-9923-a2dbf29acbb9)
































