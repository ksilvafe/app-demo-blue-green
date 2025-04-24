server = ubuntu@app-demo.duckdns.org
key = ~/.ssh/app-demo.pem
project_path = $(shell basename $(shell pwd))

rsync:
	rsync -azv -e "ssh -i $(key)" ./ $(server):~/$(project_path)

deploy: rsync
	ssh -i $(key) $(server) "cd ~/$(project_path) && docker compose down && docker compose up -d"