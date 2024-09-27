# Running MySQL Locally in a Docker Container and Connecting to MySQL Workbench

To run MySQL locally in a container and connect it with MySQL Workbench and your application, follow these steps:

## Step 1: Run MySQL in a Docker Container

1. Create a Docker network (optional but recommended) to connect MySQL and other containers (if any):
   ```bash
   docker network create mysql_network
   ```
2. Run the MySQL container with a custom username and password:
```
docker run --name mysql_container \
--network mysql_network \
-e MYSQL_ROOT_PASSWORD=root_password \
-e MYSQL_DATABASE=mysqltest \
-e MYSQL_USER=root \
-e MYSQL_PASSWORD=public \
-p 3306:3306 \
-d mysql:latest
```
## Step 2: Connect MySQL Workbench to MySQL Container

1. Open MySQL Workbench on your local machine.
2. Create a new connection:
   - Click on **Database** → **Connect to Database**.
   - In the **Hostname** field, enter `localhost` (or `mysql_container` if MySQL Workbench is running in the same Docker network).
   - In the **Port** field, enter `3306`.
   - Use `root` as the **Username** and `root_password` as the **Password** (or use `your_user` and `your_password` if you want to connect with the non-root user).
3. Click **OK** to connect.

## Step 3: Connect Your Application to MySQL

In your application, configure the database connection as follows:

- **Host**: `localhost` (or `mysql_container` if your app is running in the same Docker network).
- **Port**: `3306`.
- **Database**: `your_db`.
- **Username**: `your_user` (or `root` if you're using the root account).
- **Password**: `your_password` (or `root_password` if using the root account).

## Step 4: Verify Connection in MySQL Workbench and Application

- MySQL should now be running and accessible via MySQL Workbench on port `3306`.
- Your application should be able to connect to the MySQL database using the provided credentials.


## Install and Run MySQL Workbench on macOS via Homebrew

### Step 1: Update Homebrew
```bash
brew update
```

### Step 2: Install MySQL Workbench

```brew install --cask mysqlworkbench```

### Step 3: Launch MySQL Workbench
open /Applications/MySQLWorkbench.ap