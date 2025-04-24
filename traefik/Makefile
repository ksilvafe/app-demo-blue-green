server = ubuntu@app-demo.duckdns.org
key = ~/.ssh/app-demo.pem
project_path = $(shell basename $(shell pwd))

rsync:
	rsync -azv -e "ssh -i $(key)" ./ $(server):~/$(project_path)

setup: rsync
	ssh -i $(key) $(server) "cd ~/$(project_path) && \
		touch acme.json && \
		chmod 600 acme.json && \
		docker network create traefik || true && \
		docker compose up -d"

deploy: rsync
	ssh -i $(key) $(server) "cd ~/$(project_path) && \
		docker compose down && \
		docker compose up -d"
