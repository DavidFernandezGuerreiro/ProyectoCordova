# ProyectoCordova
Plugin para la batería del móvil. Asignatura PMDM.

1. Creé un proyecto Cordova en blanco usando la línea de comandos:
```
cordova create AppBattery
```

2. Una vez hecho esto, me situé en el directorio del proyecto. Y agregué la plataforma en la que quiero que se cree mi aplicación.
  En mi caso:
 ```
 cd AppBattery
 cordova platform add browser
 cordova platform add android
 ```
 
 3. Instalé el plugin de la batería
 ```
 cordova plugin add cordova-plugin-battery-status
 ```
 
  - Todos los eventos de este plugin devuelven un objecto con las siguientes propiedades:
    - **level**: devuelve el porcentaje de carga de la batería
    - **isPlugged**: devuelve un boolean indicando si el móvil está enchufado.
 
 4. Código del programa:
   - Se "dispara" cuando el porcentaje aumenta o disminuye en un 1%, o si el móvil está enchufado o desenchufado.
   - **index.js**:
      - Agrego el detector de eventos:
      ```
	    window.addEventListener("batterystatus", onBatteryStatus, false); 
      ```
      - Función que devuelve la llamada
      - Si se desenchufa el móvil salta un audio(alarma) antirobo.
      ```
      function onBatteryStatus(info) {
         //Salta una alerta mostrando el nivel de batería y si está conectado
         alert("ESTADO BATERIA: \n Nivel: " + info.level + " Conectado: " + info.isPlugged);

         //Si se desconecta el cargador salta una alarma
         if(info.isPlugged==false) {
            var audio = document.getElementById("audio");
            audio.play();
         } 
      }
      ```
 - **index.html**:
   - Añadí al html la etiqueta audio, que recoge la ruta del audio
   ```
    <audio id="audio" controls>
        <source type="audio/mp3" src="alarma_battery.mp3">
    </audio>
   ```
 
 
