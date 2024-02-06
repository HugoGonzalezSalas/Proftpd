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

Si descomentamos:
```
nano /etc/proftpd/proftpd.conf
  DefaultRoot ~
```
Tendiramos acceso a / al conectarnos:

![image](https://github.com/HugoGonzalezSalas/Proftpd/assets/114906900/68086a48-dc99-4626-91b1-6d5b22d1d2ab)

D) Configurar mensaje de bienvenida y error:
```
nano /etc/proftpd/proftpd.conf
  AccessGrantMsg "BIENVENIDO A MI SERVIDOR FTP, UN SALUDO DE PARTE DE HUGO."
  AccessDenyMsg "Error al conectarte al servidor FTP de Hugo."
```
![image](https://github.com/HugoGonzalezSalas/Proftpd/assets/114906900/5edde289-e29d-4e54-9111-6d95dffb8549)

## Anonymous

Para conectarse como anonymous utilizaremos la herramiento filezilla. Pero antes deberemos hacer algunas configuraciones:
```
nano /etc/proftpd/proftpd.conf
 <Anonymous ~ftp>
   User ftp
   Group nogroup
   UserAlias anonymous ftp
   DirFakeUser on ftp
   DirFakeGroup on ftp
   RequireValidShell off
   MaxClients 10

   <Directory *>
     <Limit WRITE>
       DenyAll # no podra hacer cambios en ningun directorio/archivo, solo verlos.
     </Limit>
   </Directory>
 </Anonymous>
```
A) Comprobar en Filezilla:
![image](https://github.com/HugoGonzalezSalas/Proftpd/assets/114906900/440a2ea5-1269-4efb-a34b-3b6fe556141a)

B) Cambiar de Directorio a Anonymous:
Creamos el directorio y se lo asignamos a anonymous:
```
mkdir -p /home/anonymous
chown -R ftp /home/anonymous/
```
Y en el fichero de configuracion deberemos de asignarle una nueva ruta:
```
nano /etc/proftpd/proftpd.conf
 <Anonymous /home/anonymous>
   User ftp
   Group nogroup
   UserAlias anonymous ftp
   DirFakeUser on ftp
   DirFakeGroup on ftp
   RequireValidShell off
   MaxClients 10

   <Directory *>
     <Limit READ>
       AllowAll
     </Limit>
     <Limit WRITE>
       AllowAll
     </Limit>
   </Directory>
 </Anonymous>
```
Comprobamos que podemos crear directorios y archivos en la ruta asignada desde clonezilla con anonymous:
![image](https://github.com/HugoGonzalezSalas/Proftpd/assets/114906900/b419445b-eb5e-41e8-94bc-1fe0978a28d3)

Comprobaciones en el servidor:
![image](https://github.com/HugoGonzalezSalas/Proftpd/assets/114906900/0009c70a-cf28-4ac6-a80e-62a50d64f7db)

Efectivamente se crean los archivos y directorios en la ruta asignada.




