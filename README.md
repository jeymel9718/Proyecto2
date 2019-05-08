# Proyecto2
## Prerequisitos
- [Vagrant](https://www.vagrantup.com/downloads.html)
- Virtual Box

## Inicializar VMs
Correr `$ vagrant up` para inicializar las maquinas virtuales.
_Este comando debe ser ejecutado dentro de un directorio con un **Vagrantfile**_

## Incializar Docker Swarm
### Swarm Manager
- ssh dentro del nodo manager `$ vagrant ssh manager`
- Correr `$ docker swarm init --advertise-addr 192.168.50.10:2377`
  Esto genera dos comando con un token, copiar el que sea similar a `docker swarm join --token <token> 192.168.50.10:2377`
### Swarm workers
- ssh en cada worker
   * `$ vagrant ssh worker-1` 
   * `docker swarm join --token <token> <manager-IP-address>:2377`
   * `$ exit`
   * `$ vagrant ssh worker-2`
   * `docker swarm join --token <token> <manager-IP-address>:2377`
- Ejecutar `docker node ls` en el nodo manager y comprobar

## Inicializar los servicios
- ssh en el manager
- `$ cd /vagrant/home`
- `$ docker-compose build`, esto crea una imagen necesaria para crear el cluster de mongodb
- `$ docker stack deploy -c docker-compose.yml api`, esto inicializa los servicios
- Comprobar el estado de los servicios con `$ docker stack ps api`

