# Sample application for tutorials

* goal
  * environment /
    * uses
      * complete the [grafana tutorials](https://grafana.com/tutorials)

## Prequisites

* install
  * [Docker](https://docs.docker.com/install/)
  * [Docker Compose](https://docs.docker.com/compose/install/)

## how to run?

* | this path,
  * `docker-compose up -d`
* | browser,
  * http://localhost:3000
  * "admin" / "admin"
    * Problems:
      * Problem1: 401
        * Attempt1
        ```
          $ docker exec -it --user root grafana-tutorial-environment-grafana-1 sh
          $ apk add sqlite
          $ cd /var/lib/grafana
          $ sqlite3 grafana.db "SELECT id, login, email, name, is_admin FROM user;"
          $ sqlite3 grafana.db "UPDATE user SET password = '59acf18b94d7eb0694c61e60ce44c110c7a683ac6a8f09580d626f90f0a9c285', salt = 'LhQoKvYd' WHERE login = 'admin';"
          $ sqlite3 grafana.db "SELECT login, password FROM user WHERE login='admin';"  
          $ exit
          $ docker compose restart grafana
        ```
        * Attempt2:
          ```
          docker compose down
          docker volume rm grafana-tutorial-environment_app_data
          docker compose up
          ```
        * Attempt3:
          ```
          docker run -d \
            --name grafana-test \
            -p 3000:3000 \
            -e "GF_SECURITY_ADMIN_PASSWORD=admin" \
            grafana/grafana:10.4.0
          ```
        * Solution: `brew services stop grafana`
          * Reason: 🧠I had got grafana as services ALSO running🧠
          

### disable login
* comment lines | [docker-compose.yml](docker-compose.yml)
