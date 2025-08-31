
````markdown
# go-pgsql-helper-kit

A lightweight helper kit for working with PostgreSQL in Go.  
This package provides easy database connection management and CRUD helpers.


### Installation

```bash
go get github.com/abhishekprakash256/go-pgsql-helper-kit
````



## ⚙️ Configuration

Database connection settings are stored in `config.yaml`.

Example:

```yaml
database:
  host: "localhost"
  port: 5432
  user: "abhi"
  password: "mysecretpassword"
  dbname: "test_db"
  sslmode: "disable"
```

The `cmd/main.go` file is responsible for **loading `config.yaml`** and passing the configuration into the helper package.



## 🐳 Running PostgreSQL with Docker

Start a PostgreSQL container:

```bash
docker run -d --name postgres-container \
  -e POSTGRES_USER=abhi \
  -e POSTGRES_PASSWORD=mysecretpassword \
  -e POSTGRES_DB=test_db \
  --network my_network \
  -p 5432:5432 \
  postgres
```



## Database Setup

1. Connect to the container:

   ```bash
   docker exec -it postgres-container psql -U abhi -d test_db
   ```

2. List tables:

   ```sql
   \dt
   ```

3. See table structure:

   ```sql
   \d loginTable
   \d messageTable
   ```

4. Query data:

   ```sql
   SELECT * FROM loginTable;
   SELECT * FROM messageTable;
   ```



## Project Structure

```
.
├── cmd
│   └── main.go
├── config
│   └── config.yaml   # <-- database configuration
├── pgsql
│   └── db
│       ├── connection
│       │   └── pgsql_connector.go
│       └── crud
│           ├── pgsql_crud.go
│           └── pgsql_db.go
├── go.mod
├── go.sum
└── README.md
```



## Usage Example

```go
package main

import (
	"fmt"
	"log"

	"github.com/abhishekprakash256/go-pgsql-helper-kit/pgsql/db/connection"
)

func main() {
	db, err := connection.Connect("config/config.yaml")
	if err != nil {
		log.Fatal(err)
	}
	defer db.Close()

	fmt.Println("Connected to Postgres successfully")
}
```


