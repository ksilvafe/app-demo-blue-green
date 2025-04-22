server = ec2-user@devpira.brorlandi.xyz # servidor onde vai ser conectado.
project_path = $(shell basename $(shell pwd)) # mostra pasta dentro do servidor onde vai ser criado.

rsync:
	rsync -azv . $(server):$(project_path)

# First run for setup docker compose and traefik
setup: rsync
	ssh $(server) "cd ~/$(project_path) &&\
		touch acme.json &&\
		chmod 600 acme.json &&\
	 	docker network create traefik &&\
		docker compose up -d"

deploy: rsync
	ssh $(server) "cd $(project_path) && docker compose down && docker compose up -d"