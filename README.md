MuduoChatServer

快速运行
------------
* 环境
	* Ubuntu版本20.04
	* MySQL版本8.0.29

* 测试前确认已安装MySQL数据库
    ```C++
    //MySQL登录名=root 密码=123456
    
    // 建立chat库
    create database chat;
    
    // 创建user表（存储用户）
    create table if not exists user(
      id int(11) auto_increment,
      name varchar(50) not null unique,
      password varchar(50) not null,
      state enum('online', 'offline') default 'offline',
      primary key(id)
    )engine=innodb default charset=utf8;
    
    // 创建friend表（存储好友）
    create table if not exists friend(
      userid int(11) not null,
      friendid int(11) not null,
      primary key(userid,friendid)
    )engine=innodb default charset=utf8;
    
    // 创建groupuser表（存储群成员）
    create table if not exists groupuser(
      groupid int(11) not null,
      userid int(11) not null,
      grouprole enum('creator','normal') default 'normal',
      primary key(groupid,userid)
    )engine=innodb default charset=utf8;
    
    // 创建offlinemessage表（存储离线消息）
    create table if not exists offlinemessage(
      userid int(11) not null,
      message varchar(500) not null
    )engine=innodb default charset=utf8;
    
    // 创建allgroup表（存储群）
    create table if not exists allgroup(
      id int(11) auto_increment,
      groupname varchar(50) not null unique,
      groupdesc varchar(200) default '',
      primary key(id)
    )engine=innodb default charset=utf8;
    ```   
    
* mkdir build
* 安装boost库和mysql开发包
    ```C++
    sudo apt install g++ cmake make libboost-dev
    sudo apt-get install -y build-essential
    sudo apt-get install libmysqlclient-dev
    ```    
    
* muduo库和redis的头文件，lib导入
    ```C++
    cd extra/include
    sudo cp -r * /usr/local/include
    cd extra/lib
    sudo cp * /usr/local/lib
    sudo ldconfig /usr/local/lib
    ```  
    
* build
    ```C++
    ./autobuild.sh
    ```

运行命令
------------
```C++
cd bin
./ChatServer 127.0.0.1 9006
./ChatClient 127.0.0.1 9006
```

