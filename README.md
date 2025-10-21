# 🐍 Viborita en Assembly ARM  
### TP Final – Organización del Computador  
**Grupo 02**

---

## 📘 Descripción del Proyecto
Este proyecto implementa una versión inicial del clásico juego **“Viborita”** programada en **Assembly ARM**, como trabajo práctico final para la materia *Organización del Computador*.  
El objetivo principal es demostrar el manejo del ingreso de datos, control de pantalla y lógica de movimiento utilizando llamadas al sistema (syscalls) en bajo nivel.

---

## ⚙️ Funcionamiento General
El juego corre en la consola y muestra un mapa estático con la viborita y algunos indicadores.  
El usuario puede ingresar comandos de movimiento (W, A, S, D) o salir del juego con la tecla Q.  
Cada iteración limpia la pantalla y vuelve a mostrar el estado del mapa actualizado.

---

## 🧩 Estructura Principal del Código
El programa está dividido en funciones que realizan tareas específicas:

- **borrarMapa** → Limpia la pantalla usando secuencias ANSI.  
- **imprimirMapa** → Dibuja el mapa del juego.  
- **imprimirInstrucciones** → Muestra las teclas disponibles.  
- **pedirLetra** → Captura la tecla presionada.  
- **revisarLetra** → Determina la acción a realizar según la tecla.  
- **jugar** → Orquesta el ciclo principal del juego.  
- **fin** → Limpia la pantalla y muestra un mensaje de salida.

---

## ⌨️ Ingreso de Datos
El ingreso de datos se realiza mediante la **lectura desde teclado** usando la llamada al sistema `read` (swi 0).  
El siguiente fragmento muestra cómo se obtiene la tecla ingresada por el jugador:

```asm
pedirLetra:
    push {lr}		
    mov r7, #3          // syscall: read
    mov r0, #0          
    ldr r1, =cadena     
    mov r2, #2          
    swi 0               
    pop {lr}
    bx lr
