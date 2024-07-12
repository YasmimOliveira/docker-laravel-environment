# docker-laravel-environment
This is a repository to be used as a template/guide for creating a Laravel development environment with Docker and Docker Compose.

Images used for the containers:

* PHP version 8.1 FPM
* Nginx as a reverse proxy
* MariaDB version 11.2 as the database
* Adminer as the MySQL client

### Steps to Run the Application:

1. **Create the Laravel Project**  
   Outside the "docker" folder, run the command:  
   ```bash
   composer create-project laravel/laravel laravel-app
   ```  
   *Note: The application name will be used for the Docker build folders, so any changes need to be reflected in the Dockerfiles as well.*

2. **Build the Environment**  
   Run:  
   ```bash
   docker-compose up -d --build
   ```

3. **Adjust Variables in the Laravel `.env` File as needed**  

4. **Clear Cache**  
   Outside the container:  
   ```bash
   docker exec setup-php php artisan config:cache
   ```  
   OR  
   Inside the PHP container, run the Laravel command:  
   ```bash
   php artisan config:cache
   ```

5. **Install Dependencies**  
   Outside the container:  
   ```bash
   docker exec setup-php composer install
   ```  
   OR  
   Inside the PHP container, run the Laravel command:  
   ```bash
   composer install
   ```

**Access URLs:**  
- [http://localhost:8888/](http://localhost:8888/) -> Adminer  
- [http://localhost:8080/](http://localhost:8080/) -> Application



### Resources/Links Used to Create the Environment:

- [YouTube Tutorial - João Lucas Xavier - Ambiente de desenvolvimento Laravel com Docker, Docker compose, MySQL, PhpMyAdmin e Redis](https://youtu.be/E4-IfMSZCVc)
- [Docker Hub](https://hub.docker.com/)
- [Laravel Documentation](https://laravel.com/docs/11.x/)
- [Medium Article](https://medium.com/@marcosdiasdev/criando-um-ambiente-docker-para-desenvolvimento-laravel-com-php-nginx-e-mysql-847490acc50d)
- [Full Cycle Tutorial](https://fullcycle.com.br/docker-e-docker-composer-na-pratica-criando-ambiente-laravel/)
- [DigitalOcean Guide](https://www.digitalocean.com/community/tutorials/how-to-containerize-a-laravel-application-for-development-with-docker-compose-on-ubuntu-18-04-pt)
