NGINX proxy - Kerberos - Elasticsearch
--------------------------------------

- Build and start
docker-compose build
docker-compose up

- Add role to kerb-user (pwd: esadmin)
curl -u yg -H "Content-Type: application/json" -XPOST http://localhost:9200/_xpack/security/role_mapping/kerbrolemapping -d '{ "roles" : [ "monitoring_user" ], "enabled": true, "rules" : { "field" : { "username" : "kerb-user@DEV.LOCAL" } } }'

- login to client
docker exec -t -i <kerberos-client> /bin/bash
kinit kerb-user@DEV.LOCAL
curl --negotiate -u : http://proxy.proxy-kerberos-elasticsearch_dev.local:9200

