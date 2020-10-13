# Redis-6.0.8-ARMv7
Download, Compile, and Install Redis 6.0.8 for ARMv7 on Ubuntu 16.04 LTS.

1. Install build-essential packages for armhf:   
dpkg-dev: Debian package development tools  
g++: GNU C++ compiler  
gcc: GNU C compiler  
libc6-dev: GNU C Library: Development Libraries and Header Files  
make: utility for directing compilation  

2. Install tcl 8.5 or newer in order to run the Redis test make.

3. Download, extract and compile Redis 6.0.8 with:
```
$ wget https://download.redis.io/releases/redis-6.0.8.tar.gz
$ tar xzf redis-6.0.8.tar.gz
$ cd redis-6.0.8
$ make
```
4. Run make test to make sure everything was built correctly:
```
$ make test
```
5. Install Redis:
```
$ make install
```
6. Configure Redis:
```
$ sudo mkdir /etc/redis
$ sudo cp ./redis.conf /etc/redis
$ sudo nano /etc/redis/redis.conf
```
set supervised systemd  
set dir /var/lib/redis  
set maxmemory 100mb  
set maxmemory-policy allkeys-lru  

7. Create Redis Service:
Create /etc/systemd/system/redis.service file to get started:
```
sudo nano /etc/systemd/system/redis.service
```
8. Create Redis User, Group and Working Directory:
```
$ sudo mkdir /var/lib/redis
$ sudo adduser --system --group --no-create-home redis
$ sudo chown redis:redis /var/lib/redis
$ sudo chmod 770 /var/lib/redis
```
9. Start and Test Redis:
```
$ sudo systemctl start redis
$ sudo systemctl status redis
$ redis-cli
127.0.0.1:6379> ping
PONG
```
10. Enable Redis as Startup Service:
```
$ sudo systemctl enable redis
Created symlink from /etc/systemd/system/multi-user.target.wants/redis.service to /etc/systemd/system/redis.service.
```
