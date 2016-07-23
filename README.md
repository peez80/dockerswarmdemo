node-1: 192.168.33.111
node-2: 192.168.33.112
node-3: 192.168.33.113

node1:

docker swarm init --listen-addr 192.168.33.111:2377

docker network create --driver overlay app



node2:
 
 docker swarm join --secret 9pbttqdki8emau6vcuujjngeh \
         --ca-hash sha256:b6d45455f864e2f3cd977cdb47cad5a2bbae9a9743ef6bae3465320adeeb5c81 \
         --listen-addr 192.168.33.112:2377 \
         192.168.33.111:2377
         
node3: 
 docker swarm join --secret 9pbttqdki8emau6vcuujjngeh \
         --ca-hash sha256:b6d45455f864e2f3cd977cdb47cad5a2bbae9a9743ef6bae3465320adeeb5c81 \
         --listen-addr 192.168.33.113:2377 \
         192.168.33.111:2377



docker service create --name outerservice --replicas 3 --network app -p 80:80 peez/outerservice
docker service create --name innerservice --replicas 2 --network app peez/innerservice



--constraint my.example="specialrole"

--mode=global 