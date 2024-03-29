# GroceryOnline
The application enables users and admins to create and manage grocery items while also facilitating the creation of sale orders.

## Feature Overview
The app supports two roles: ADMIN and USER

Admin Responsibilities:
- Add new grocery items to the system 
- View existing grocery items         
- Remove grocery items from the system 
- Update details (e.g., name, price) of existing grocery items
- Manage inventory levels of grocery items 

User Responsibilities:
- View the list of available grocery items 
- Ability to book multiple grocery items in a single order

## Tools and Tech Stack
- Java: JDK 17
- Framework: Spring Boot 3.2, Spring Web, Spring Security
- ORM: Hibernate
- Database: MySQL 8
- Build tool: Maven 3.6, Docker
- API docs: Swagger

## Installation
Clone git repo
```shell
git clone git@github.com:sourabh14/GroceryOnline.git
```

Update spring datasource username and password in src/main/resources/application.properties
The default datasource url is set to localhost:3306

Mysql:
```mysql
create database groceryonline;
```

Start the application:
```shell
cd GroceryOnline
./mvnw spring-boot:run
```

### Installation through Docker
```shell
docker network create groceryonline-network
docker pull mysql
docker run --name mysql-container --network groceryonline-network -p 3306:3306 -e MYSQL_ROOT_PASSWORD=uniware -d mysql
mysql -h localhost -P 3306 --protocol=tcp -u root -p
create database groceryonline;
```

```shell
export JAVA_HOME="$(/usr/libexec/java_home -v 17)"
mvn clean package -Dmaven.test.skip
docker build -t grocery-online:0.0.1 .
docker run --name app-container --network groceryonline-network -p 8081:8081 grocery-online:0.0.1
```

## Usage

#### Sign-up for admin user
The request payload includes the username and password, and upon submission, a JWT token is returned in response. 
![](src/main/resources/images/SignUp.png)

This token functions as the user's identity and must be passed in request headers while making subsequent API calls.
![](src/main/resources/images/JwtTokenHeader.png)

#### Add an item
The role-based authorization ensures that, only admin users are allowed to add an item. 
![](src/main/resources/images/AddItem.png)

#### Update item inventory
The update-type can be ADD, REMOVE or REPLACE 
![](src/main/resources/images/UpdateInventory.png)

#### Create sale order
![](src/main/resources/images/CreateSaleOrder.png)

## Api Docs
Api docs generated via swagger are available at:
[http://localhost:8081/swagger-ui/index.html](http://localhost:8081/swagger-ui/index.html)

![](src/main/resources/images/ApiDocs.png)

