# Prerequisites:
* [Docker](https://store.docker.com/search?type=edition&offering=community)
* [docker-compose](https://docs.docker.com/compose/install/)
* [git](https://git-scm.com/downloads)
* [jq](https://stedolan.github.io/jq/download/)
* [Postman](https://www.getpostman.com/apps)

# Preparatory steps:
```bash
$ git clone git@github.com:joosepm/elab.git
```
Download NASA access logs from  http://ita.ee.lbl.gov/html/contrib/NASA-HTTP.html

Set mmapfs parameters in your environment:
``` bash
$ sysctl -w vm.max_map_count=262144
```
