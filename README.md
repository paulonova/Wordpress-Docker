# Wordpress Docker

Tutorial link: https://www.hostinger.com/tutorials/run-docker-wordpress

### Create a folder with the project name

1 - create a new docker-compose.yml file, and paste the contents below:

<samp>
  version: "3"
    # Defines which compose version to use
    services:
      # Services line define which Docker images to run. In this case, it will be MySQL server and WordPress image.
      db:
        image: mysql:5.7
        # image: mysql:5.7 indicates the MySQL database container image from Docker Hub used in this installation.
        restart: always
        environment:
          MYSQL_ROOT_PASSWORD: MyR00tMySQLPa$$5w0rD
          MYSQL_DATABASE: MyWordPressDatabaseName
          MYSQL_USER: paulonova
          MYSQL_PASSWORD: paulonova
          # Previous four lines define the main variables needed for the MySQL container to work: database, database username, database user password, and the MySQL root password.
      phpmyadmin:
        image: phpmyadmin/phpmyadmin:latest
        restart: always
        environment:
          PMA_HOST: db
          PMA_USER: root
          PMA_PASSWORD: root
        ports:
          - "8080:80"

    wordpress:
    depends_on: - db
    image: wordpress:latest
    restart: always # Restart line controls the restart mode, meaning if the container stops running for any reason, it will restart the process immediately.
    ports: - "8000:80" # The previous line defines the port that the WordPress container will use. After successful installation, the full path will look like this: http://localhost:8000
    environment:
    WORDPRESS_DB_HOST: db:3306
    WORDPRESS_DB_USER: paulonova
    WORDPRESS_DB_PASSWORD: paulonova
    WORDPRESS_DB_NAME: MyWordPressDatabaseName # Similar to MySQL image variables, the last four lines define the main variables needed for the WordPress container to work properly with the MySQL container.
    volumes: ["./:/var/www/html"]
    volumes:
    mysql: {}

</samp>

2 - Run docker compose up -d

- It will install the latest wordpress and all docker dependencies include Phpmyadmin as database
