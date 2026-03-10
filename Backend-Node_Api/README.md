# To Run Application without containers
# First Run postgresql database inside container
```
docker run -d \
--name db
-e POSTGRES_PASSWORD=shankar \
-v pgdata:/var/lib/postgresql/data \
-p 5432:5432 \
postgres:15.1-alpine
```
# To run Node-api without Containers
```bash
nvm ls
nvm use node 19.4
npm install
export DATABASE_URL=postgresql://postgres:shankar@localhost:5432/postgres
npm run dev
```
