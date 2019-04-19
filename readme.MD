docker login demo.goharbor.io -u michaelmi@vmware.com

cd /home/michmike/github/HarborDemo/alpinesql
docker build -t demo.goharbor.io/hrteam/headtrax:1.0 .
docker push demo.goharbor.io/hrteam/headtrax:1.0

cd /home/michmike/github/HarborDemo/ubuntusql
docker build -t demo.goharbor.io/hrteam/headtraxsql:2.1 .
docker push demo.goharbor.io/hrteam/headtraxsql:2.1

cd /home/michmike/github/HarborDemo/unpatched
docker build -t demo.goharbor.io/hrteam/centosbaseimage:1.0 .
docker push demo.goharbor.io/hrteam/centosbaseimage:1.0

cd /home/michmike/github/HarborDemo/patched
docker build -t demo.goharbor.io/hrteam/centosbaseimage:2.1 .
docker push demo.goharbor.io/hrteam/centosbaseimage:2.1

docker rmi demo.goharbor.io/hrteam/centosempty:1.0
docker rmi demo.goharbor.io/hrteam/centosempty:1.1
docker rmi demo.goharbor.io/hrteam/centosempty:1.2
docker rmi demo.goharbor.io/hrteam/centosbaseimage:1.0
docker rmi demo.goharbor.io/hrteam/headtrax:1.0
docker rmi centos:7

export DOCKER_CONTENT_TRUST=1
export DOCKER_CONTENT_TRUST_SERVER=https://demo.goharbor.io
docker tag demo.goharbor.io/hrteam/headtrax:1.0 demo.goharbor.io/hrteam/signedmaster:3.2
docker push demo.goharbor.io/hrteam/signedmaster:3.2
export DOCKER_CONTENT_TRUST=0
