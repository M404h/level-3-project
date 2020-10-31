network:
	docker network create -d bridge catanet

bulid:
	docker build -t ma404/catalogue .
	docker build -t ma404/catalogue-db ./docker/catalogue-db/

run:
	docker run -itd --net catanet ma404/catalogue-db
	docker run -itd --net catanet -p 8081:80 ma404/catalougue

