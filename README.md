# ProFTP


## 1.- Instalacion De ProFTP
Actualizamos la maquina e instalamos Proftp y Ftp
```
apt upgdate -y
apt upgrade -y
apt install proftpd -y
apt install ftp -y
```

## 2.- Configuración y Personalización de Proftp
A) Personalizamos el Proftp:
```
nano /etc/proftpd/proftpd.conf
  ServerName "HugoProFTP"
  # Set to inetd only if you would run proftpd by inetd/xinetd/socket.
  # Read README.Debian for more information on proper configuration.
  ServerType standalone
  DeferWelcome off
```
B) Para que cada usuario trabaje en su directorio /home tendremos que asegurarnos de que esta comentada la siguiente linea:
```
nano /etc/proftpd/proftpd.conf
 # DefaultRoot ~
```
C) Añadimos un nuevo usuario para conectarnos a ftp:
```
adduser hugogs
```
D) Comprobamos la conectividad
```
 ftp 172.31.28.32 #ip de tu maquina/servidor
```
![image](https://github.com/HugoGonzalezSalas/Proftpd/assets/114906900/f1058cb8-f415-4088-b877-2a09708e1124)

D) Configurar mensaje de bienvenida y error:
```
nano /etc/proftpd/proftpd.conf
  AccessGrantMsg "BIENVENIDO A MI SERVIDOR FTP, UN SALUDO DE PARTE DE HUGO."
  AccessDenyMsg "Error al conectarte al servidor FTP de Hugo."
```
![image](https://github.com/HugoGonzalezSalas/Proftpd/assets/114906900/5edde289-e29d-4e54-9111-6d95dffb8549)



