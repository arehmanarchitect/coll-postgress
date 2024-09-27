# Running PostgreSQL Locally in a Docker Container and Connecting to pgAdmin

To run PostgreSQL locally in a container and connect it with pgAdmin and your application, follow these steps:

## Step 1: Run PostgreSQL in a Docker Container

1. Create a Docker network (optional but recommended) to connect PostgreSQL and pgAdmin:
   ```bash
   docker network create pg_network
   ```
2. Run the PostgreSQL container with the username `root` and password `public` and sample db `posgres`:
```
docker run --name postgres_container \
--network pg_network \
-e POSTGRES_USER=root \
-e POSTGRES_PASSWORD=public \
-e POSTGRES_DB=postgres \
-p 5432:5432 \
-d postgres
```
This command will:
* Set the POSTGRES_USER to root.
* Set the POSTGRES_PASSWORD to public.
* Set the POSTGRES_DB to your desired database name here `postgres` but you can change.
* Expose PostgreSQL on port 5432 (local) to 5432 (container).

## Step 2: Run pgAdmin in a Docker Container

Run pgAdmin in another container to manage your PostgreSQL database:
```
docker run --name pgadmin_container1 \
--network pg_network \
-e PGADMIN_DEFAULT_EMAIL=admin@example.com \
-e PGADMIN_DEFAULT_PASSWORD=admin_password \
-p 8081:80 \
-d dpage/pgadmin4
```
This command will:
* Set the pgAdmin admin email and password.
* Expose pgAdmin on port 8081 on your local machine.

## Step 3: Connect pgAdmin to PostgreSQL

1. Open your browser and go to [http://localhost:8081](http://localhost:8081).
2. Log in with the email `admin@example.com` and password `admin_password` you set in Step 2.
3. Add a new server:
   - Right-click on "Servers" → Create → Server.
   - Enter a name for the server.
   - In the "Connection" tab:
     - **Host**: `postgres_container` (container name, since both containers are on the same network).
     - **Port**: `5432`.
     - **Username**: `root`.
     - **Password**: `public`.

## Step 4: Connect Your Application to PostgreSQL

In your application, configure the database connection as follows:

- **Host**: `localhost` (or `postgres_container` if your app is running in the same Docker network).
- **Port**: `5432`.
- **Database**: `your_db`.
- **Username**: `root`.
- **Password**: `public`.

Your PostgreSQL instance should now be available locally and accessible via pgAdmin and your application.

Let me know @email `arehman.architect@gmail.com`if you need further assistance!