# Checkpoint: Mi primer laboratorio seguro de ciberseguridad

Reporte técnico del laboratorio Lab-Ubuntu 2. Windows 11 anfitrión y Ubuntu 24.04 LTS invitado. VirtualBox 7.2.22, 4 GB RAM, 2 CPU y 25 GB de disco. Se reutilizó la VM anterior.

## Red NAT

Configuré el adaptador en NAT para permitir actualizaciones sin exponer directamente la VM a la red física. NAT reduce las conexiones entrantes no solicitadas, siempre que no se configure reenvío de puertos; no constituye aislamiento absoluto del anfitrión.

![Red NAT](capturas/01-evidencia.png)

## Usuario estándar

En Windows 11 (equipo anfitrión), creé la cuenta local Practicas y seleccioné Usuario estándar. La separación de cuentas limita los cambios administrativos.

![Usuario estándar](capturas/02-evidencia.png)

## Windows Update

Windows Update muestra que todo está actualizado al momento de la captura. Las actualizaciones corrigen vulnerabilidades conocidas.

![Windows Update](capturas/03-evidencia.png)

## Usuario sin privilegios

Creé el usuario practicas con adduser. Los comandos id, getent passwd y groups muestran la cuenta y sus grupos practicas y users, sin pertenencia a sudo.

![Usuario sin privilegios](capturas/04-evidencia.png)

## Permisos del archivo

Creé laboratorio.txt y apliqué chmod 600. El comando ls -l muestra -rw-------: el propietario puede leer y escribir, mientras el grupo y otros usuarios no tienen permisos.

![Permisos del archivo](capturas/05-evidencia.png)

## Gestión de actualizaciones

Ejecuté sudo apt update, sudo apt upgrade -y y apt list --upgradable. La consulta fue exitosa; libsqlite3-0 quedó pendiente por el despliegue gradual (phasing). No se afirma que todos los paquetes estén actualizados.

![Gestión de actualizaciones](capturas/06-evidencia.png)

## Firewall activo

Habilité UFW y comprobé su estado con sudo ufw status verbose. Está activo al arranque y deniega conexiones entrantes por defecto, permitiendo las salientes.

![Firewall activo](capturas/07-evidencia.png)

## Instantáneas de seguridad

Con la VM apagada, creé Clean Install - Hardening applied y Hardening inicial, conservando Instalación Base Limpia. Las instantáneas permiten recuperar el estado guardado. La descripción registra red aislada, firewall y permisos restringidos.

![Instantáneas de seguridad](capturas/08-evidencia.png)

## Restricción de sudo

La prueba ping confirma conectividad. El intento de ejecutar sudo desde practicas fue rechazado, demostrando la restricción administrativa.

![Restricción de sudo](capturas/09-evidencia.png)

## Fallo inicial de conectividad

La consulta inicial falló por resolución de nombres. Cambié la red a NAT y posteriormente completé la consulta de repositorios, como se muestra en la evidencia 06.

![Fallo inicial de conectividad](capturas/10-evidencia.png)

## Conclusión

El mínimo privilegio, la gestión de actualizaciones, el firewall y las instantáneas permiten reducir riesgos y recuperar el laboratorio ante errores.
