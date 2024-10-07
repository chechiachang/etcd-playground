up:
	docker-compose up -d

down:
	docker-compose down

# dangerous
destroy: down
	docker volume rm etcd1 etcd2 etcd3
	rm -rf etcd*/*
