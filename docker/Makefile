build:
	docker build -t libssh_server .
start: stop
	docker run --name libssh_server -p 2222:2222/tcp libssh_server
stop:
	docker stop libssh_server
	docker rm libssh_server
clean: stop
	docker image rm libssh_server
