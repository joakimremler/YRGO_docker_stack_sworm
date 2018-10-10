## L2 Grupp arbete?

what is a stack?
what is a docker-compose?

- port
- volumes
  What is a swarm?

## Assignments

In this lession we are going to learn about Docker Stack and Sworm. This includes how to start a Sworm cluster and to create and run stacks.

## 1. Initialize docker swarm

The first thing we should do is to [initialize](https://docs.docker.com/engine/reference/commandline/swarm_init/#extended-description) a docker swarm on our Droplet. You also need to `advertise` with your Droplet ip adress.
`docker swarm init --advertise-addr ip_to_droplet`

When you do this you will get a snippet that you can use to connect multiply nodes to this sworm. Save that snippet to later use.

## 2. Create a Docker Stack

After initialize a Docker sworm we can start using [Docker stack](https://docs.docker.com/get-started/part5/#introduction). Our first stack is going to be our `kalleanka/loop` that we did [build](https://docs.docker.com/engine/reference/commandline/build/#tarball-contexts) in previous lession. If you cannot find it when you type `docker image ls` then you need to build this image. When you got this image you can create a stack file called `loop.yml` and add service `loop` with a image called `kalleanka/loop`. You should use stack file version `3.6`.

Run this file with `docker stack deploy -c loop.yml loop`. To see if service is running you can [list](https://docs.docker.com/engine/reference/commandline/service_ls/#related-commands) all services. You can also enter a specific service with `docker stack services <name_of_stack>`.

When you see that all services is running you should watch the [logs](https://docs.docker.com/engine/reference/commandline/logs/#usage) from this process with a parameter `-f`.

`docker logs -f <name_of_stack>`

## 3. Visualizer stack

When you have a Docker swarm it is nice to have a tool that can monitor all processes in real time. This is where we can use [visualizer](https://github.com/dockersamples/docker-swarm-visualizer).
You should create a new stack file named `visualizer.yml` and add visualizer and export [port](https://docs.docker.com/compose/compose-file/#pid) `5000`. Then you should [deploy](https://docs.docker.com/engine/reference/commandline/deploy/#parent-command) this service with service name `visualizer`.
Monitor this new service in your browser on your `droplet_ip` on port `5000`.

## 3. Stack with Wordpress and mysql

Create a stackfile called `wordpress.yml` this should contain a [wordpress](https://hub.docker.com/_/wordpress/) installation and mysql database. [Deploy](https://docs.docker.com/engine/reference/commandline/deploy/#parent-command) this with name `wordpress`.

When you se that this service is up and running you should [remove](https://docs.docker.com/engine/reference/commandline/stack_rm/) this stack.

## 4. Save data when container restarts

Good work! You have now a working wordpress installation, but the problem is now when you restart your container your installation will disappear. To fix this we need to store all mysql data inside a [volume](https://docs.docker.com/docker-cloud/apps/stack-yaml-reference/#target_num_containers). So add a volume to `mysql` service inside `wordpress.yml`.

## 5. PhpMyAdmin

Add [phpmyadmin](https://hub.docker.com/r/phpmyadmin/phpmyadmin/) to `wordpress.yml` and change port setup to `8181:80`. Deploy `wordpress` stack file and complete `Wordpress` installation.

## 6. Scale up and down

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
