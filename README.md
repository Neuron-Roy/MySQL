![Discord](https://img.shields.io/discord/974657490874679306?color=7289DA&label=Discord&style=for-the-badge)
![Website](https://img.shields.io/website?style=for-the-badge&up_message=Visit%20nyrone.net&url=https%3A%2F%2Fnyrone.net)

# MySQL
this is a guide to create users with password on mysql database in linux ubuntu 20.04 LTS Server

# Step - 1
**Basic Login??**

if you are in Windows 10 or 11 look up for `command prompt` in the start menu and open it

![Search](https://cdn.discordapp.com/attachments/982008692746616832/982748148982251570/unknown.png)

if you are on WIndows 11 you might this kind of interface

![image](https://cdn.discordapp.com/attachments/982008692746616832/982748865398714398/unknown.png)

type the command in the command prompt
```
ssh root@123.123.123.123
```
Replace `123.123.123.123` with your server ip
and now you are in your linux server *thank me join my discord lol*

# Step - 2
**Change the IP Bindings so that you can connect to the Database using the Server ip**

**One of the more common problems that users run into when trying to set up a remote MySQL database is that their MySQL instance is only configured to listen for local connections. This is MySQL’s default setting, but it won’t work for a remote database setup since MySQL must be able to listen for an external IP address where the server can be reached. To enable this, open up your `mysqld.cnf` file**

```bash 
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf 
```
find a line begins with the bind-address . It will look like this:

```cnf
lc-messages-dir = /usr/share/mysql
skip-external-locking
#
# Instead of skip-networking the default is now to listen only on
# localhost which is more compatible and is not less secure.
bind-address            = 127.0.0.1 <<-- Change this to 0.0.0.0
```
change `bind-address = 127.0.0.1` to `bind-address = 0.0.0.0` and save it by using `CTRL + S` and close using `CTRL + X` 

After that restart MySQL *(Just In case if you have mariadb installed restart mariadb too)*
```
systemctl restart mysql
systemctl restart mariadb
```

# Step - 3
**connect to mysql**
`mysql -u root -p` (press enter twice)
it should look somthing like this:

![image](https://cdn.discordapp.com/attachments/982008692746616832/982744089353158656/unknown.png)

if not do `use mysql;` after that it look like the image above

# Step - 4
**Creating DataBase Users**

Replace `qbc` with any username you like

Replace `RandomPass8980!` with any password you like

Replace `123.123.123.123` with your Server ip

```SQL
CREATE USER 'qbc'@'localhost' IDENTIFIED BY 'RandomPass8980!';

CREATE USER 'qbc'@'%' IDENTIFIED BY 'RandomPass8980!';

CREATE USER 'qbc'@'123.123.123.123' IDENTIFIED BY 'RandomPass8980!';

GRANT ALL PRIVILEGES ON *.* TO 'qbc'@'localhost' WITH GRANT OPTION;

GRANT ALL PRIVILEGES ON *.* TO 'qbc'@'%' WITH GRANT OPTION;

GRANT ALL PRIVILEGES ON *.* TO 'qbc'@'123.123.123.123' WITH GRANT OPTION;
```
