## streamcat-api

#### Tech Stack
* Go1.5.1
* Echo - Micro Web framework
* sqlx - sql layer extensions to golang's database/sql
* sqlite3 support
* go-validator - model/struct validations
* jwt-go - JWT implementation library

### Go Setup (for local development)
* [Install Go](https://golang.org/dl/)
```
brew install go
export GOPATH=~/Source/Go
export PATH=$PATH:$GOPATH/bin
```

## GoDep
```
go get github.com/tools/godep
cd ~/Source/Go/src/streamcat-api
godep restore
godep save ./...
```


### Project Setup (for local development)

* Setup GOPATH project structure
```
cd ~/Source/Go
git clone github.com/streamcatTV/streamcat-api src
cd src/streamcat-api
go get -d -v ./...
go build streamcat-api && ./streamcat-api
```

```
Running with 8 CPUs
Starting server on port 4000
```

* Setup auto-reload (optional)
```
go get github.com/codegangsta/gin
cd src/stream-api
gin -a 4000 -p 4001
```

### Database Setup

#### SQLite
* Create DB (sqlite3)
```
sqlite3 test.db < scripts/schema.sql
```

#### PostgreSQL
```
# Backup
pg_dump -Fc -h db.streamcat.tv -U postgres -d streamcat > postgres-schema.bak
pg_dump -Ft -h db.streamcat.tv -U postgres -d streamcat > postgres-schema.tar

# Restore
pg_restore -Fc -h db.streamcat.tv -U postgres -d streamcat postgres-schema.bak
pg_restore -Ft -h db.streamcat.tv -U postgres -d streamcat postgres-schema.tar

# Dump schema only
pg_dump -s -h db.streamcat.tv -U postgres -d streamcat > postgres-schema.sql

# Restore schema only
pg_restore -s -h db.streamcat.tv -U postgres -d streamcat postgres-schema.sql
```


http://postgresguide.com/utilities/backup-restore.html


### Docker Setup

Create your Docker Machine, or use the default env.

`eval "$(docker-machine env default)"`

```
git clone streamcat-api
docker build -t streamcat-api .
docker run -p 8080:4000 -d streamcat-api
```

Load `localhost:8080` into your browser. If you are using a Docker VM, use the VM's IP address instead. i.e. `192.168.99.100:8080`

You can view the active VM by running `docker-machine ls`

Load `http://localhost:4001/` in the browser. Code will hot-reload on browser refresh when code changes.



### Go IDE Resources
* https://github.com/fatih/vim-go
* https://github.com/farazdagi/vim-go-ide
* http://farazdagi.com/blog/2015/vim-as-golang-ide/
* https://atom.io/packages/go-plus
* https://github.com/joefitzgerald/go-plus
* https://github.com/nsf/gocode
