# Название выполняемого задания
Создать домашнюю сетевую лабораторию. Изучить основы DNS, научиться работать с технологией Split-DNS в Linux-based системах

# Текст задания
1. взять стенд https://github.com/erlong15/vagrant-bind 
добавить еще один сервер client2
завести в зоне dns.lab имена:
web1 - смотрит на клиент1
web2  смотрит на клиент2
завести еще одну зону newdns.lab
завести в ней запись
www - смотрит на обоих клиентов

2. настроить split-dns
клиент1 - видит обе зоны, но в зоне dns.lab только web1
клиент2 видит только dns.lab



# Описание
Запускаем по классике 
```bash
vagrant up
```

# Как проверить
Так как реализовывал по методички и там требовалась перекрыть /etc/bind/named.conf, показываю результат тестирования split-dns, но файлы все приложил.

Итак checklist методички.

Подключаемся к Client1
```bash
root@client1:~# ping www.newdns.lab
PING www.newdns.lab (192.168.60.15) 56(84) bytes of data.
64 bytes from 192.168.60.15: icmp_seq=1 ttl=64 time=0.036 ms
64 bytes from 192.168.60.15: icmp_seq=2 ttl=64 time=0.160 ms
^C
--- www.newdns.lab ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1013ms
rtt min/avg/max/mdev = 0.036/0.098/0.160/0.062 ms
root@client1:~# ping web1.dns.lab
PING web1.dns.lab (192.168.60.15) 56(84) bytes of data.
64 bytes from 192.168.60.15: icmp_seq=1 ttl=64 time=0.032 ms
64 bytes from 192.168.60.15: icmp_seq=2 ttl=64 time=0.046 ms
64 bytes from 192.168.60.15: icmp_seq=3 ttl=64 time=0.051 ms
^C
--- web1.dns.lab ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2086ms
rtt min/avg/max/mdev = 0.032/0.043/0.051/0.008 ms
root@client1:~# ping web2.dns.lab
ping: web2.dns.lab: Name or service not known
root@client1:~# 
```

Подключаемся к Client2
```bash
root@client2:~# ping www.newdns.lab
ping: www.newdns.lab: Name or service not known
root@client2:~# ping web2.dns.lab
PING web2.dns.lab (192.168.60.16) 56(84) bytes of data.
64 bytes from 192.168.60.16: icmp_seq=1 ttl=64 time=0.030 ms
64 bytes from 192.168.60.16: icmp_seq=2 ttl=64 time=0.084 ms
^C
--- web2.dns.lab ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1019ms
rtt min/avg/max/mdev = 0.030/0.057/0.084/0.027 ms
```