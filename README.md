# docker-nginx-containers-network

Containers Communication In A Network
-------------------------------------
Two containers can communicate with each other when they are in same network. Below are the steps to achieve the communication between containers in a network.

1. Create and View network.
2. Create nginx image.
3. Run the image created in step 2 as container mynginx1 with user defined network created in step 1.
   * Verify that container is running. 
4. Run the image created in step 2 as container mynginx2 with user defined network created in step 1.
    * Verify that container is running. 
5. Access each container using curl.
6. Verify each container attached to user defined network.
7. Go into the container mynginx1. Ping to the mynginx2. 
8. Go into the container mynginx2. Ping to the mynginx1.
9. Getting logs of each of the container.
9. Remove resources.
    * Stop the both of the containers.
    * Remove the images.
    * Remove the network.
    
Create and View network
-----------------------
* create: `sudo docker network create --driver bridge my_nw`
* view: `sudo docker network ls`

![image](https://user-images.githubusercontent.com/17001948/44581949-6df17b80-a7bd-11e8-84a1-d8b0ce469595.png)

Create Nginx Image
------------------
* Download this repository. Go to the repostiroy directory. Open the terminal.
* create image: `sudo docker build -t my-nginx-image .`
![image](https://user-images.githubusercontent.com/17001948/44582806-62538400-a7c0-11e8-899e-a253e9d2e246.png)
You will see below screen while running the above command.
![image](https://user-images.githubusercontent.com/17001948/44582827-7bf4cb80-a7c0-11e8-9d48-43f3f33c6cc8.png)
Imgae create successfully
![image](https://user-images.githubusercontent.com/17001948/44582856-99c23080-a7c0-11e8-9cc5-979fe96b9691.png)

* view: `sudo docker images`
![image](https://user-images.githubusercontent.com/17001948/44582903-bc544980-a7c0-11e8-92ec-6a4706e214a1.png)

Run Image As Container(mynginx1) By Attaching With The Network Name
---------------------------------------------------------
* run : `sudo docker run --rm --name mynginx1 --network="my-nw" -d -p 81:80 my-nginx-image`
* view: `sudo docker ps`
* mynginx1 is exposed to 81 port of the localhost.

Run Image As Container(mynginx2) By Attaching With The Network Name
------------------------------------------------------------------
* run : `sudo docker run --rm --name mynginx2 --network="my-nw" -d -p 82:80 my-nginx-image`
* view: `sudo docker ps`
* mynginx2 is exposed to 82 port of the localhost.
![image](https://user-images.githubusercontent.com/17001948/44584886-10aef780-a7c8-11e8-83dc-7706eeec2c84.png)


Access Each Container Using Curl
--------------------------------
* curl(mynginx1) : `curl http://localhost:81`
![image](https://user-images.githubusercontent.com/17001948/44583516-4a313400-a7c3-11e8-9463-4c34af79f201.png)

* curl(mynginx2) : `curl http://localhost:82`
![image](https://user-images.githubusercontent.com/17001948/44583530-5cab6d80-a7c3-11e8-8de5-1f98c03ee760.png)

Verify Each Container Attached To Network
------------------------------------------
* inspect mynginx1 container : `sudo docker container inspect mynginx1`
![image](https://user-images.githubusercontent.com/17001948/44584942-3b994b80-a7c8-11e8-9152-662a876bf2f5.png)
* inspect mynginx2 container : `sudo docker container inspect mynginx2`
![image](https://user-images.githubusercontent.com/17001948/44585015-7b603300-a7c8-11e8-9017-fd2f935cf099.png)

For both of the containers you can see the network name is `my-nw`.

Go Into Container mynginx1 and Access mynginx2
----------------------------------------------
* `sudo docker exec -it mynginx1 bash`
![image](https://user-images.githubusercontent.com/17001948/44584724-81a1df80-a7c7-11e8-9f2a-bd525d7f82e5.png)
* Access mynginx2 from container mynginx1. See I am using container name instead container's ip.`curl http://mynginx2:80`
![image](https://user-images.githubusercontent.com/17001948/44585120-e4e04180-a7c8-11e8-922a-b2d2572b2232.png)
* validate if ping is working or not. Ping will show the network name as `my-nw`. `ping mynginx2`
![image](https://user-images.githubusercontent.com/17001948/44585208-283ab000-a7c9-11e8-812f-a0d2c05d7024.png)
* exit from the container `mynginx1`. `exit`
![image](https://user-images.githubusercontent.com/17001948/44585251-51f3d700-a7c9-11e8-943e-5e1aee68b3a6.png)

![image](https://user-images.githubusercontent.com/17001948/44585256-591ae500-a7c9-11e8-9fec-ce11baa37315.png)

Go Into Container mynginx2 and Access mynginx1
----------------------------------------------
* Screenshots for this use case is similar to above. So I am not attaching again.
* `sudo docker exec -it mynginx2 bash`
* Access mynginx1 from container mynginx2. See I am using container name instead container's ip.`curl http://mynginx1:80`
* validate if ping is working or not. `ping mynginx2`
* exit from the container `mynginx1`. `exit`

Remove Resources
-----------------------------------------
* stop containers: `sudo docker stop mynginx1 mynginx2` . This will stop and remove the containers as we have started the containers with --rm flag. verify if containers are removed or not: `sudo docker ps`and then `sudo docker ps -a`.
![image](https://user-images.githubusercontent.com/17001948/44585554-64badb80-a7ca-11e8-971d-7ba0fa7bec9c.png)
We are seeing some old containers but not the containers mynginx1 and mynginx2.

* delete image: `sudo docker rmi my-nginx-image`. Verify if image is deleted or not. `sudo docker images` .
![image](https://user-images.githubusercontent.com/17001948/44585640-a8154a00-a7ca-11e8-9bb3-3a1b719b4a76.png)
After delete. we are not seeing our image `my-nginx-image`.

* delete network: `sudo docker network rm my-nw`. Verify if network is deleted or not. `sudo docker network ls`.
After delete, we wont able to see the network my-nw.
![image](https://user-images.githubusercontent.com/17001948/44585744-f7f41100-a7ca-11e8-95c1-e5e47ebb6e17.png)

What Next?
----------------------
Practice again from the beggining of this document.
