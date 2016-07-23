node-1: 192.168.33.111

node-2: 192.168.33.112

node-3: 192.168.33.113

node1:

    docker swarm init --listen-addr 192.168.33.111:2377

    docker network create --driver overlay app



node2:
 
     docker swarm join --secret THE_SECRET \
         --ca-hash sha256:THE_HASH \
         --listen-addr 192.168.33.112:2377 \
         192.168.33.111:2377
         
node3:
 
     docker swarm join --secret THE_SECRET \
         --ca-hash sha256:THE_HASH \
         --listen-addr 192.168.33.113:2377 \
         192.168.33.111:2377
         
node4:
 
     docker swarm join --secret THE_SECRET \
         --ca-hash sha256:THE_HASH \
         --listen-addr 192.168.33.114:2377 \
         192.168.33.111:2377
         
         
node5:
 
     docker swarm join --secret THE_SECRET \
         --ca-hash sha256:THE_HASH \
         --listen-addr 192.168.33.115:2377 \
         192.168.33.111:2377


Services

    docker service create --name outerservice --replicas 3 --network app -p 80:80 peez/outerservice
    docker service create --name innerservice --replicas 2 --network app peez/innerservice



    --constraint my.example="specialrole"

    --mode=global 