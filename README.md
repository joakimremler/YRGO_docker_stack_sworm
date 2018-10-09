## L2 Grupp arbete?

what is a stack?

- port
- volumes
  What is a swarm?

1. Docker stack
   add this to a stack file called `my_first_stack_file`

- build Kalleanka loop to image

* docker swarm init
* save snippet
* create a stack file called `loop.yml`
* docker stack deploy -c loop.yml loop
* docker logs -f

1. New Stack with visulizater (https://github.com/dockersamples/docker-swarm-visualizer)

- docker stack deploy -c visualizer.yml visualizer
- docker stack services visualizer
- Check in browser

3. Create a stackfile called `wordpress` with wordpress and mysql (https://hub.docker.com/_/wordpress/)

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
