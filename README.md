Plataphorma
===========

Meteor pet project created to teach my students the following Meteor functionality: 

* Collection's publish/subscribe 
* Deps.autorun 
* Meteor.methods/call 
* Integration of non-Meteor code in compatibility folder (HTML5 games Alien Invasion and Froot Wars)
* Usage of allow to control client access to collections

![ScreenShot](/screenshot.png)


Plataphorma offers the possibility to run 2 different HTML5 games: Alien Invasion and Froot Wars. 

On the right side of the screen the best players of each game are shown, updated in real time each time a signed in player finishes a game. If no game is selected, the best players overall are shown.

On the left side of the screen a chatroom for the current game is available. Only signed in users can post messages. If no game is selected a general chatroom is shown.

The original code of the two HTML5 games integrated in this project is available here:
* Alien Invasion: https://github.com/cykod/AlienInvasion
* Froot Wars: http://www.wrox.com/WileyCDA/WroxTitle/Professional-HTML5-Mobile-Game-Development.productCd-1118301323,descCd-DOWNLOAD.html

Bootstrap style (file bootstrap.min.css) provided by http://bootswatch.com


Running the project
-------------------

A live version of this code is running here: http://plataphorma.meteor.com

To run the project locally, clone the repo and run ```meteor``` inside it. You can see in .meteor/packages that this Meteor project uses these packages:
* ```meteor remove autopublish```
* ```meteor remove insecure```
* ```meteor add bootstrap```
* ```meteor add accounts-ui```
* ```meteor add accounts-password```


PREGUNTAS
=========

1) Click en botón de juego:
Cada vez que se hace click sobre un botón de juego se ejecutan las líneas correspondientes a cada click, estando éstas entre la línea
112 y la línea 130 del fichero client.js. Cuando se hace click sobre el juego AlienInvasion, el botón se encuentra dentro de un div con 
id="games" class="btn-group". Y dentro de éste, un input con id="AlienInvasion" class="btn btn-primary". Cuando se ejecutan las
líneas correspondientes con el juego AlienInvasion en el client.js, se oculta el juego FrootWars y se muestra el canvas de nuestro juego.


2) Se escribe mensaje chat sin estar autenticado:
Se ejecutan las líneas 84-105. Al escribir el mensaje sin estar autenticado dentro de las líneas citadas, al no estar dentro de la base
de datos de usuarios de Meteor, se va por la rama else (línea 101). Esta línea lo que hace es llamar a un div con id="login-error", el cual 
crea un texto que te informa para que te registres y un botón con una X, para eliminar ese texto.


3) Se escribe mensaje chat estando autenticado:
Se ejecutan las líneas 84-105. Al escribir el mensaje estando autenticado, Meteor guarda el valor del id de usuario y el valor del
mensaje creado justo antes de dar al enter. El mensaje se introduce ejecutándose las líneas 56-57 del index.html con id="message". 
Si el valor del mensaje es distinto de null, se inserta en la base de datos Messages, al que se le asocia el id de usuario, la fecha y
el juego en el que se produce el mensaje. A partir de aquí se actualizan todos los publish.


4) Se termina partida con puntuación positiva sin estar autenticado:
Al terminar la partida se produce un cambio reactivo, en la plantilla best_players. Se obtiene la partida del juego al que estamos jugando
y se comprueba si estamos autenticados. En este caso, no se agrega la puntuación a la plantilla puesto que no estamos autenticados.


5) Se termina partida con puntuación positiva estando autenticado:
Es el caso contrario al 4. Se agrega la puntuación a la plantilla best_players.


6) ¿Qué sale en consola cuando te autenticas (sig in)?:
"current user: null"
"current user: v7kKhDaZnspeTNrKo"
Se ejecutan las líneas 56-61 del fichero client.js, currentUser es una fuente reactiva lo que quiere decir que se
modifica el id de usuario cada vez que un usuario se autentica y gracias a la función autorun esto se produce automáticamente.

7) ¿Qué sale en consola cuando sales (sign out)?:
"current user: null"
Se ejecutan las líneas 56-61 del fichero client.js, currentUser es una fuente reactiva lo que quiere decir que se
modifica el id de usuario cada vez que un usuario se autentica. Si un usuario sale de la plataforma, currentUser toma el valor de null,
lo que significa que no se devuelve ningún id de usuario.
