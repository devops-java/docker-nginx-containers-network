# docker-nginx-containers-network

Containers Communication In A Network
-------------------------------------
Two containers can communicate with each other when they are in same network. Below are the steps to achieve the communication between containers in a network.

1. Create and View network.
2. Create nginx image.
3. Run the image created in step 2 as container mynginx1 with user defined network created in step 1.
   * Verify that container is running. 
   * Access it using curl.
4. Run the image created in step 2 as container mynginx2 with user defined network created in step 1.
    * Verify that container is running. 
    * Access it using curl.
5. Go into the container mynginx1. Ping to the mynginx2. 
6. Go into the container mynginx2. Ping to the mynginx1.
7. Remove resources.
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


