## L2 Grupp arbete?

what is a stack?
what is a docker-compose?

- port
- volumes
  What is a swarm?

  [<img src="https://media.giphy.com/media/jYjA6fHBfAZvq/giphy.gif" alt="Docker" width="100%">](https://www.docker.com/)

## Assignments

In this lession we are going to learn about Docker Stack and Swarm. This includes how to start a Swarm cluster and to create and run stacks.

## 1. Initialize docker swarm

The first thing we should do is to [initialize](https://docs.docker.com/engine/reference/commandline/swarm_init/#extended-description) a docker swarm on our Droplet. You also need to `advertise` with your Droplet [ip adress](https://www.computerhope.com/unix/uifconfi.htm).
`docker swarm init --advertise-addr ip_to_droplet`

When you do this you will get a snippet that you can use to connect multiply nodes to this swarm. Save that snippet to later use.

## 2. Create a Docker Stack

After initialize a Docker swarm we can start using [Docker stack](https://docs.docker.com/get-started/part5/#introduction). Our first stack is going to be our `kalleanka/loop` that we did [build](https://docs.docker.com/engine/reference/commandline/build/#tarball-contexts) in previous lession. If you cannot find it when you type `docker image ls` then you need to rebuild this image.

When you got this image you can create a [stack file](https://docs.docker.com/get-started/part5/#add-a-new-service-and-redeploy) called `loop.yml` and add service `loop` with a image called `kalleanka/loop`. You should use stack file version `3.6`.

Run this file with `docker stack deploy -c loop.yml loop`. To see if service is running you can [list](https://docs.docker.com/engine/reference/commandline/service_ls/#related-commands) all services. You can also list a specific service with `docker stack services <name_of_stack>`.

## 3. Visualizer stack

When you have a Docker swarm it is nice to have a tool that can monitor all processes in real time. This is where we can use [visualizer](https://github.com/dockersamples/docker-swarm-visualizer).
You should create a new stack file named `visualizer.yml` and add visualizer and export [port](https://docs.docker.com/compose/compose-file/#pid) `5000`.

Then you should [deploy](https://docs.docker.com/engine/reference/commandline/deploy/#parent-command) this service with service name `visualizer`.

Monitor this `Visualizer` tool by entering your `droplet_ip` and port `5000` in your browsers url.

## 3. Stack with Wordpress and mysql

Create a new stackfile called `wordpress.yml` this should contain a [wordpress](https://hub.docker.com/_/wordpress/) installation and mysql database. [Deploy](https://docs.docker.com/engine/reference/commandline/deploy/#parent-command) this with name `wordpress`.

When you se that this service is up and running on `Visualizer` you should [remove](https://docs.docker.com/engine/reference/commandline/stack_rm/) the `wordpress` stack.

## 4. Save data when container restarts

Good work! You have now a working wordpress installation, but the problem is now when you restart your container your installation will disappear. To fix this we need to store all mysql data inside a [volume](https://docs.docker.com/docker-cloud/apps/stack-yaml-reference/#target_num_containers). So add a volume to [mysql service](https://stackoverflow.com/questions/39175194/docker-compose-persistent-data-mysql) inside `wordpress.yml`.

## 5. PhpMyAdmin

Add [phpmyadmin](https://hub.docker.com/r/phpmyadmin/phpmyadmin/) to `wordpress.yml` and change port setup to `8181:80`. Deploy `wordpress` stack file and complete `Wordpress` installation. [Insperation](https://github.com/andreaskoch/dockerized-magento/issues/18).

Run `docker stack services wordpress` to se that all services get started.

## 6. Scale up and down

Now we should scale up our `Kalleanka loop` application by (deploy)(https://docs.docker.com/get-started/part5/#add-a-new-service-and-redeploy) to `replicas: 3`. This will duplicate our stack container to three replicas. You can scale up and down without restarting service.

## 6. Loadbalancer

The final moment in this lession is to [expand](https://docs.docker.com/engine/swarm/swarm-tutorial/add-nodes/) your swarm to multiply Droplets. Do this with the snippet you got in the first assament. There is multiply ways of doing this but eider you create a new Droplet and add that to your cluster och you borrow a Droplet from a classmate. When you have done this watch your `Visualizer` where you can se that Docker swarm acts as a Loadbalancer between multiply Droplets.

https://media.giphy.com/media/jYjA6fHBfAZvq/giphy.gif

# OLD

When you see that all services is running you should watch the [logs](https://docs.docker.com/engine/reference/commandline/logs/#usage) from this process with a parameter `-f`.

`docker logs -f <name_of_stack>`
