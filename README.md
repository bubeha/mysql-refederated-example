### Turning FEDERATED engine on:

`
SHOW ENGINES;
`

### Create server statement in the master database server

`
CREATE SERVER server_name
FOREIGN DATA WRAPPER mysql
OPTIONS (USER 'your_user', PASSWORD 'your_password', HOST 'your_host', DATABASE 'your_database_name', PORT 3306);
`


### Create table in the another database server

`
CREATE TABLE your_table (
  id int NOT NULL AUTO_INCREMENT,
  created_at timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (id),
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT
`

### Create table in the master database server

`
CREATE TABLE your_federated_table (
    id INT NOT NULL AUTO_INCREMENT,
    created_at TIMESTAMP NULL DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (id),
)  ENGINE=FEDERATED DEFAULT CONNECTION='server_name/your_table'
`

### Create view in the master database server

`
CREATE VIEW your_view_name AS
    SELECT 
        *
    FROM
        your_table 
    UNION ALL SELECT 
        *
    FROM
        your_federated_table
`