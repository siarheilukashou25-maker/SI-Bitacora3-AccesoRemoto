# Bitacora-Tecnica-IV.-Laboratorio-de-Teletransportacion-Digital-SSH-y-RDP-

  

## Primer problema

  

    @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    
    @ WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED! @
    
    @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    
    IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
    
    Someone could be eavesdropping on you right now (man-in-the-middle attack)!
    
    It is also possible that a host key has just been changed.
    
    The fingerprint for the ED25519 key sent by the remote host is
    
    SHA256:9laUg9PnAijNshh6J/2kooTcUBlKjeXHzpypq12EcXc.
    
    Please contact your system administrator.
    
    Add correct host key in C:\\Users\\DAM1/.ssh/known_hosts to get rid of this message.
    
    Offending ECDSA key in C:\\Users\\DAM1/.ssh/known_hosts:3
    
    Host key for [localhost]:2222 has changed and you have requested strict checking.
    
    Host key verification failed.
    
    PS C:\Users\DAM1\Desktop\Bitacora 4\Bit-cora-T-cnica-IV.-Laboratorio-de-Teletransportaci-n-Digital-SSH-y-R

  

Este es el primer problema con cual me he conectado. Esto ocurre porque ya tenia constrasena para @localhost y puerto 2222 creado cunado estaba conectando atraves de powershell a la VM de Ubuntu server. Para arreglarlo tenemos que ir a 

> C:\Users\DAM1\ .ssh

 y borrar todo el contenido de la carpeta.

  --------------------

Despues ya podemos conectarnos atraves de comando `ssh alumno@localhost -p 2222`

  

    DP-> ssh alumno@localhost -p 2222
    
    The authenticity of host '[localhost]:2222 ([::1]:2222)' can't be established.
    
    ED25519 key fingerprint is SHA256:9laUg9PnAijNshh6J/2kooTcUBlKjeXHzpypq12EcXc.
    
    This key is not known by any other names.
    
    Are you sure you want to continue connecting (yes/no/[fingerprint])? y
    
    Please type 'yes', 'no' or the fingerprint: yes
    
    Warning: Permanently added '[localhost]:2222' (ED25519) to the list of known hosts.

  Si no tenemos la constrasena nos va a salir siguiente error
  ![Captura de login incorrecto](https://i.imgur.com/Zi65NIR.png)

Despues de introducir la constrasena correcta ya vamos a estar conectados.
![Captura de estar conectado](https://i.imgur.com/3uHmaFW.png)

--------------------
Crearemos par de llaves:

 
    PS C:\Users\DAM1> ssh-keygen -t ed25519 -C "qwe@qwe.com"
    Generating public/private ed25519 key pair.
    Enter file in which to save the key (C:\Users\DAM1/.ssh/id_ed25519): qwe
    Enter passphrase (empty for no passphrase):
    Enter same passphrase again:
    Your identification has been saved in qwe
    Your public key has been saved in qwe.pub
    The key fingerprint is:
    SHA256:ESb6iIB4G+g9QkbYmDCxa1hSPGLItz1u9N3Hzbh8vtk qwe@qwe.com
    The key's randomart image is:
    +--[ED25519 256]--+
    |OB. . o          |
    |XB+. . o .       |
    |O+=.+ .          |
    |=*.= * .         |
    |o+oo+ + S . . +  |
    |. . .o . . . + o |
    | . o .           |
    | o .o            |
    | o+E             |
    +----[SHA256]-----+
    PS C:\Users\DAM1>

--------------------

    CMD+R > MSTSC > localhost:3389
![Error de escritorio remoto](https://i.imgur.com/5Xz1vZI.png)

Esto ocurre porque RDP intenta abrir una sesión de consola en *localhost*, pero esa sesión ya está ocupada — precisamente por la sesión en la que estás trabajando ahora mismo. Windows no permite abrir una segunda sesión de consola en el mismo equipo.

-----
**Captura de ssh_config**
![ssh_config](https://i.imgur.com/QMuNE8c.png)
-----
**Captura de prueba realizada**
![Prueba lograda](https://i.imgur.com/7vNk5ZR.png)
