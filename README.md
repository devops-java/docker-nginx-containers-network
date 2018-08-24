# docker-nginx-containers-network

Containers Communication In A Network
-------------------------------------
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
