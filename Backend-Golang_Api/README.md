# To Run Golang-api without Containers
```bash
mkdir go-workspace
export GOPATH=$PWD/go-workspace
go mod download
export DATABASE_URL=postgresql://postgres:shankar@localhost:5432/postgres
go run main.go
```
