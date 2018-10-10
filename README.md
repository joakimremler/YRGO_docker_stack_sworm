## L2 Grupp arbete?

what is a stack?
what is a docker-compose?

- port
- volumes
  What is a swarm?

## Assignments

In this lession we are going to learn about Docker Stack and Sworm. This includes how to start a Sworm cluster and to create and run stacks.

## 1. Initialize docker swarm

The first thing we should do is to [initialize](https://docs.docker.com/engine/reference/commandline/swarm_init/#extended-description) a docker swarm on our Droplet. You need also to `advertise` your Droplet ip adress.

When you do this you will get a snippet that you can use to connect multiply nodes to this sworm. Save that snippet.

`docker swarm init --advertise-addr ip_to_droplet`

## 2. Create a Docker Stack

After initialize a Docker sworm we can start using [Docker stack](https://docs.docker.com/get-started/part5/#introduction). Our first stack is going to be our `kalleanka/loop` that we did [build](https://docs.docker.com/engine/reference/commandline/build/#tarball-contexts) in previous lession. If you cannot find it when you type `docker image ls` then you need to build this image. When this has been done create a file called `loop.yml` and add service `loop` with a image called `kalleanka/loop`. You should use stack file version `3.6`.

Run this file with `docker stack deploy -c loop.yml loop`. To see if service is running you can [list](https://docs.docker.com/engine/reference/commandline/service_ls/#related-commands) all services. You can also enter a specific service with `docker stack services <name_of_stack>`.

When you see that all services is running you should watch the [log](https://docs.docker.com/engine/reference/commandline/logs/#usage) from this process with a parameter `-f`.

`docker logs -f <name_of_stack>`

## 3. Visulizater stack

When you have a Docker swarm it is nice to have a tool that can monitor all processes in real time. This is where we can use [Visulizater](https://github.com/dockersamples/docker-swarm-visualizer).
You should create a new stack file named `visulizater.yml` and add visualizer and export [port](https://docs.docker.com/compose/compose-file/#pid) `5000`. Then you should [deploy](https://docs.docker.com/engine/reference/commandline/deploy/#parent-command) this service with service name `visualizer`.
Monitor this new service in your browser on your `droplet_ip` on port `5000`.

3. Create a stackfile called `wordpress.yml` with wordpress and mysql (https://hub.docker.com/_/wordpress/)

- Wordpress
- mysql
- docker stack deploy -c wordpress.yml wordpress
- docker stack rm wordpress

3b. add volume that data dosent disepers when reboot

- Add volume to mysql data

4. Add phpmyadmin to wordpress.yml (https://hub.docker.com/r/phpmyadmin/phpmyadmin/)

- change port to phpmyadmin to 8181
- Make a Wordpress installation

5. Scale up`Kalleanka loop` applications (deploy)(https://docs.docker.com/get-started/part5/#add-a-new-service-and-redeploy)
   - scale witout stopping
   - edit in stack.yml add `deploy: replicas: 3`
6. Create a docker swarm on multiply nodes

- copy snippet to new nodes
- se all stacks
- se live logs
- se loadbalancer
- Nginx

https://media.giphy.com/media/jYjA6fHBfAZvq/giphy.gif
