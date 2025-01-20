# Curso de C# con .NET y Angular

## Videos Destacados
* ### Seccion 2
    * Video 29: Creacion de un Componente
    * Video 30: Parametros en Componentes
    * Video 33: Proyeccion Entre vistas
    * Video 36: Fijar un head 
    * Video 37: Clases dinamicas
    * Video 38: Funciones Transformadoras
    * Video 40: Estilos globales

* ### Seccion 3
    * Video 45: Rutas (Ruteo)
    * Video 46: Inyeccion Dependencias
    * Video 47: Capturar id o valor mediante url

* ### Seccion 4
    * Video 52: Formularios Rectivos
    * Video 53: Validaciones por default 
    * Video 55: Programacion similar a la POO - Importante volver a ver 
    * Video 58: Cargar imagenes
    * Video 60: Cargar ubicaciones mapa
    * Video 61 62 y 63: Filtros
    * Video 65: Seleccion Multiple (Super Complejo)
    * Video 67: Casi me saca un ojo de la cara ese mlp (perdon)
    * Video 68: Drag and Drop

* ### Seccion 5 (Todos Son Importantes)
    * Video 73: Controladores y acciones
    * Video 75: Parametros a una accion por url
    * Video 76: Redireccion de solicitudes
    * Video 81: Parametros a una accion por otras fuentes  (formularios, json, etc, queryStrings(api/generos/id=5$nombre=Accion))
    * Video 82 83 84(ValidacionesPersonzalidasAtributos) 85(VaPeAcc): Validaciones: El "requiere" simple al declarar un atributo en una clase funciona validando que al instaciar 
    la clase entonces yo declarar ese atributo, pero esto es a nivel de codigo. Por eso se utiliza este tipo de validaciones
    * 85 y 86: Importantes, Dependencias

* ### Seccion 6
    * Video : 
    




---
---

## Comandos del Curso de C#
* ### Angular

> Angular CLI (Command Line Interface) es una herramienta oficial proporcionada por el equipo de Angular que facilita la creación, configuración y gestión de proyectos Angular. Funciona desde la línea de comandos y permite realizar diversas tareas relacionadas con el desarrollo de aplicaciones Angular de manera rápida y eficiente.

> Cada vez que se cambie el archivo de angular.json hay que volver a compilar

* ng serve -o: Compilar aplicacion de angular para ser ejecutada. El **-o** se encarga de abrir el navegador

* ng generate component libros/listado-libros  --skip-tests --dry-run
    > Es comando me permite crear un nuevo componente, por defecto se crearan en la carpeta src/apps
    * --skip-test: Salta los archivos para hacer test
    * --dry-run: Me muestra que va a crear sin hacerlo

*ng add @angular/material: Me permite instalar librerias, en este caso instalamos angular material