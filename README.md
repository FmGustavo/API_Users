# API_Users
docker run -d -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=mysql@123 mysql:latest

docker exec -it mysql mysql -u root -

name: Node.js CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    services:
      mysql:
        image: mysql:8.4
        env:
          MYSQL_ROOT_PASSWORD: 'mysql@123'
          MYSQL_DATABASE: 'usersdb'
        ports:
          - 3306:3306
    env:
        MYSQL_HOST: 'localhost'
        MYSQL_USER: 'root'
        MYSQL_PASSWORD: 'mysql@123'
        MYSQL_DATABASE: 'usersdb' 

    steps:
    - uses: actions/checkout@v2
    - name: Use Node.js
      uses: actions/setup-node@v1
      with:
        node-version: '18'
    - name: Install dependencies
      run: npm install
    - name: Start MySQL
      run: sudo /etc/init.d/mysql start
    - name: Run Db
      run: node script_db.js   
    - name: Run tests
      run: npm test
