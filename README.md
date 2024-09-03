# API_Users
docker run -d -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=mysql@123 mysql:latest

docker exec -it mysql mysql -u root -

const connection = mysql.createConnection({
host: 'localhost',
user: process.env.mysql, // Usa variáveis de ambiente
password: process.env.mysql@123,
database: process.env.usersdb
});