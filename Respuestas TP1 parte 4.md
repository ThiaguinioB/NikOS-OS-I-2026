* **¿Qué problema resuelve SSH?**
SSH (Secure Shell) resuelve el problema de la comunicación insegura a través de redes que no son de confianza. Permite a un operador administrar un sistema de forma remota cifrando de extremo a extremo todo el tráfico (comandos, respuestas y credenciales). Esto reemplaza a protocolos antiguos y vulnerables (como Telnet), que transmitían toda la información en texto plano.

* **¿Qué diferencia existe entre autenticación mediante contraseña y mediante clave pública?**
La autenticación por contraseña requiere que el usuario ingrese un secreto que viaja por la red (aunque vaya cifrado por el canal) y es susceptible a ataques de fuerza bruta o de diccionario. La autenticación por clave pública utiliza criptografía asimétrica: el cliente demuestra su identidad resolviendo un desafío matemático enviado por el servidor utilizando su clave, sin transmitir jamás el secreto mismo a través de la red.

* **¿Cuál es la función de la clave privada? ¿Y de la pública?**
* **Clave pública:** Es como un candado abierto. Se puede compartir libremente y se coloca en los servidores a los que deseas acceder (`sector-core`). Su función es cifrar desafíos que solo la clave privada correspondiente puede resolver.
* **Clave privada:** Es la llave única de ese candado. Se guarda únicamente en la máquina del operador (`field-terminal`) y se utiliza para descifrar los mensajes y firmar criptográficamente la identidad del usuario.

* **¿Dónde conoce el servidor las claves autorizadas?**
El servidor (en este caso, tu Ubuntu Server) almacena las claves públicas en las que confía dentro de un archivo oculto específico de cada usuario. Este archivo se encuentra por defecto en la ruta `~/.ssh/authorized_keys` del directorio personal del usuario (por ejemplo, `/home/thiaguinhob/.ssh/authorized_keys`).

* **¿Por qué la clave privada no debe copiarse al servidor?**
Porque la clave privada es tu prueba absoluta de identidad. Si la copias al servidor y este llega a ser vulnerado, el atacante robará tu clave privada y podrá suplantar tu identidad, obteniendo acceso automático a cualquier otra máquina de la ciudad o sector donde hayas configurado esa misma llave.

* **¿Qué riesgo implica permitir acceso remoto directo como root?**
El usuario `root` tiene permisos absolutos, pudiendo saltarse cualquier regla de protección de memoria o archivos en el sistema. Permitir su acceso remoto directo le facilita el trabajo a los atacantes, ya que saben exactamente qué nombre de usuario atacar (root) y solo necesitan vulnerar su método de autenticación para comprometer la máquina entera. La práctica segura es deshabilitar este acceso, obligando a los operadores a entrar con un usuario estándar (como `thiaguinhob`) y recién entonces escalar privilegios usando `sudo`, lo cual, además, deja un rastro claro en los registros de auditoría sobre quién ejecutó cada acción.
