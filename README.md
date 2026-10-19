# Práctica 3: Protocolos de red LAN

**Laboratorio de Comunicaciones Industriales** · Universidad Pontificia Comillas – ICAI · Edición 2026
**Alumnos:** Isabel Llorca González, Ramón Polvorosa del Campo
**Profesor:** Emilio Manuel Domínguez Adán
**Fecha de realización:** 19/10/2026

Capturas de Wireshark analizadas en el informe de la práctica. Se realizaron en la red de alumnos de la Universidad (`alu.upcont.es`), desde un portátil conectado por Wi‑Fi (IP 10.120.148.8).

## Contenido

| Fichero | Contenido | Preguntas | Tramas clave |
|---|---|---|---|
| `comillas.pcapng` | Acceso a https://www.comillas.edu (7 182 paquetes) | 4–8 | 1240–1243 (DNS), 1371 (TCP servidor → alumno) |
| `comillas_descifrado.pcapng` | Segunda captura de comillas.edu con descifrado TLS (29 481 paquetes) | 8, apartado 4.10 | 16059–16066 (HTTP/2 descifrado) |
| `websiteos.pcapng` | Descarga de http://help.websiteos.com/websiteos/example_of_a_simple_html_page.htm (1 863 paquetes) | 9–11 | 962 (GET), 976–977 (200 OK, gzip) |
| `Direccionamiento.pcapng` | Captura con las tablas ARP y DNS vacías (2 344 paquetes) | 12–14 | 295–296 (ARP), 1650–1651 (DNS) |

## Cómo abrirlas

Se abren con [Wireshark](https://www.wireshark.org/) (Archivo → Abrir). Filtros útiles:

```
ip.src == 108.157.113.6 && ip.dst == 10.120.148.8
tls.handshake.extensions_server_name == "www.comillas.edu"
http
arp.src.proto_ipv4 == 10.120.148.8 || arp.dst.proto_ipv4 == 10.120.148.8
dns.qry.name == "help.websiteos.com"
```

## Nota sobre el descifrado TLS

Por seguridad, **no se incluye el fichero de claves `sslkeys.log`**: contiene los secretos de todas las sesiones HTTPS del navegador durante la práctica. Sin él, las conexiones HTTPS aparecen como *Application Data*. Las cabeceras Ethernet, IP y TCP de las preguntas 4–8 viajan en claro y pueden verificarse igualmente. El tráfico de `websiteos.pcapng` es HTTP sin cifrar.
