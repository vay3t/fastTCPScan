# fastTCPScan

En este repositorio, os comparto la herramienta `FastTcpScan` que nos desarrollamos en la máquina `Hawk` de la plataforma [HackTheBox](https://hackthebox.eu). Esta herramienta consiste en un escáner que permite detectar de forma rápida y precisa los puertos TCP que una máquina tiene abiertos.

Para aquellos que quieran ver el desarrollo de la herramienta paso a paso, tenéis disponible el siguiente vídeo en el que la creamos desde 0:

- [Máquina Hawk - HackTheBox](https://www.youtube.com/watch?v=7L1WNU7fBec)

## ¿Cómo se usa la herramienta?

Lo primero una vez contemos con el script `fastTCPScan.go`, será compilarlo. Esto podemos hacerlo de la siguiente forma:

```go
┌─[✗]─[root@parrot]─[/home/s4vitar/Desktop]
└──╼ #cd /usr/bin/
┌─[root@parrot]─[/usr/bin]
└──╼ #go build -ldflags "-s -w" fastTCPScan.go 
┌─[root@parrot]─[/usr/bin]
└──╼ #upx brute fastTCPScan
                       Ultimate Packer for eXecutables
                          Copyright (C) 1996 - 2018
UPX 3.95        Markus Oberhumer, Laszlo Molnar & John Reiser   Aug 26th 2018

        File size         Ratio      Format      Name
   --------------------   ------   -----------   -----------
upx: brute: FileNotFoundException: brute: No such file or directory
   2260992 ->    868864   38.43%   linux/amd64   fastTCPScan                   

Packed 1 file.
```

Una vez hecho, ya podremos usar la herramienta. Su uso es de lo más sencillo, cabe decir antes que nada que la herramienta cuenta con un panel de ayuda:

```go
┌─[✗]─[root@parrot]─[/home/s4vitar/Desktop]
└──╼ #fastTCPScan -h
Usage of fastTCPScan:
  -host string
        Host o dirección IP a escanear (default "127.0.0.1")
  -range string
        Rango de puertos a comprobar: 80,443,1-65535,1000-2000, ... (default "1-65535")
  -threads int
        Número de hilos a usar (default 1000)
  -timeout duration
        Segundos por puerto (default 1s)
```

Mediante el parámetro `-host` especificamos la dirección ip de la máquina objetivo (también podemos especificar un nombre de dominio), con el parámetro `-threads` especificamos el número de hilos a usar y con el parámetro `-range` especificamos el rango de puertos a escanear.

En este caso a modo de ejemplo, efectuaremos un escaneo contra la dirección ip `192.168.11.12` haciendo uso de 900 hilos (por defecto se escanean todos los puertos [**1-65535**]):

```go
┌─[✗]─[root@parrot]─[/home/s4vitar/Desktop]
└──╼ #fastTCPScan -host 192.168.11.12 -threads 900

[*] Escaneando host 192.168.11.12 (Puerto: 1-65535)

443: Abierto
902: Abierto
3000: Abierto
```

Y listo, no tiene mayor misterio.
