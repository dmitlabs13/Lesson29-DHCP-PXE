# Lesson29-DHCP-PXE

## Задание
Настроить загрузку по сети дистрибутива Ubuntu 24\
Установка должна проходить из HTTP-репозитория.\
Настроить автоматическую установку c помощью файла user-data\
Задания со звёздочкой*\
Настроить автоматическую загрузку по сети дистрибутива Ubuntu 24 c использованием UEFI\

## Решение

В proxmox собираем две виртуальные машины.\
В обоих машина будет по две сетевые карты.\
одна карта для нашего к ним подключения, вторые карты как раз в сети где будет работать dhcp и pxe сервер.\

сеть с dhcp 10.0.0.0/24\
alp-pxeserver 10.0.0.20
alp-pxeclient - будет получать адрес от dhcp сервера\

## ставим dhcp server
```
sadmin@alp-pxeserver:~$ sudo apt update
sudo apt install isc-dhcp-server -y
```

```
sadmin@alp-pxeserver:~$ cat /etc/default/isc-dhcp-server
# Defaults for isc-dhcp-server (sourced by /etc/init.d/isc-dhcp-server)

# Path to dhcpd's config file (default: /etc/dhcp/dhcpd.conf).
#DHCPDv4_CONF=/etc/dhcp/dhcpd.conf
#DHCPDv6_CONF=/etc/dhcp/dhcpd6.conf

# Path to dhcpd's PID file (default: /var/run/dhcpd.pid).
#DHCPDv4_PID=/var/run/dhcpd.pid
#DHCPDv6_PID=/var/run/dhcpd6.pid

# Additional options to start dhcpd with.
#       Don't use options -cf or -pf here; use DHCPD_CONF/ DHCPD_PID instead
#OPTIONS=""

# On what interfaces should the DHCP server (dhcpd) serve DHCP requests?
#       Separate multiple interfaces with spaces, e.g. "eth0 eth1".
INTERFACESv4="enp6s19"
#INTERFACESv6=""
```

