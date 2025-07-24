# Systemd

### Linux systemd service

* system service: `/etc/systemd/system/xxx.service` -> `/usr/lib/systemd/system/xxx.service`
  1. root user
  2. `sudo systemctl enable xxx.service`
  3. config files auto generates in `/etc/xxx/`
  4.
* user service to all users: `/etc/systemd/user/xxx.service` -> `/usr/lib/systemd/user/xxx.service`
  1. service avaiable to all users at once
  2.
* user service to specific user: `~/.config/systemd/user/xxx.service`
  1. `systemctl --user enable xxx.service`
  2. need have its own config files if it's a self-defined service
  3. ```
     journalctl --user -u custom.service
     ```

if `sudo yum install httpd`, then for a specific service xxx, its config file is in `/etc/xxx/`

```bash
/etc/xxx/conf  # main file is /etc/xxx/conf/xxx.conf
/etc/xxx/conf.d
/etc/xxx/conf.modules.d
/etc/xxx/logs
/etc/xxx/modules
/etc/xxx/run
/etc/xxx/state
```

[Placing httpd config outside /etc/httpd/conf](https://stackoverflow.com/questions/45288872/placing-httpd-config-outside-etc-httpd-conf)

[How to create a systemd service in Linux](https://linuxhandbook.com/create-systemd-services/)

[Systemd 入门教程：实战篇](https://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-part-two.html)

[systemd user services and systemctl --user](https://nts.strzibny.name/systemd-user-services/)

[centos7上搭建http服务器以及设置目录访问](https://www.cnblogs.com/snake553/p/8856729.html)





nginx executable locates in `/usr/sbin`, and `/sbin` is a symlink of it. So we can run using `/usr/sbin/nginx`.

nginx's behavior is determined by the config file. By default, it's `/etc/nginx/nginx.conf`. But if you don't have permission to edit it, you can specify an alternative configuration and error file:

```
/usr/sbin/nginx -c <my_nginx.conf> -e <my_error.log>
```

On system reboots, we need to relaunch the above process. Thus we can config nginx as service using system managers, such as `systemd`, `init` or `upstart`. It can run and manage nginx executable by creating services.



