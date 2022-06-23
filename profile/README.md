# Requerimientos de Sistema

## Índice

- [1. Introducción](#1-introducción)
  - [1.1. Glosario](#11-glosario)
  - [1.2. Requerimientos de usuario](#12-requerimientos-de-usuario)
- [2. Requerimientos de Sistema](#2-requerimientos-de-sistema)
  - [2.1. Arquitectura de sistema](#21-arquitectura-de-sistema)
- [3. Especificaciones](#3-especificaciones)
  - [3.1. Registro de cuenta](#31-registro-de-cuenta)
  - [3.2. Inicio de sesión](#32-inicio-de-sesión)
  - [3.3. Búsqueda de entradas](#33-búsqueda-de-entradas)
  - [3.4. Valorar una entrada](#34-valorar-una-entrada)
  - [3.5. Responder una valoración](#35-responder-una-valoración)
- [4. Gráficas](#4-gráficas)
  - [4.1. Modelo Relacional](#41-modelo-relacional)
  - [4.2. Flujo de Usuario](#42-flujo-de-usuario)
- [5. Mockup](#5-mockup)
- [6. Apéndice](#6-apéndice)

## 1. Introducción

El propósito de este documento es describir las bases fundamentales, en lo que a requerimientos respecta, sobre los que se desarrollará un foro de discusión centrado en una base de datos orientada al mundo cinematográfico con características típicas de una red social para compartir reseñas y opiniones. 

Bajo esta idea a lo largo del documento abordaremos, en primera instancia, los atributos que queremos encuentre el usuario en nuestra página, tanto de manera directa como las acciones que tendrá a sus disposición y de manera indirecta como el espacio que queremos brindar en la comunidad. Posteriormente veremos los detalles prácticos que se necesitarán para poder realizar el foro como: arquitectura de sistema, flujo de acciones y modelos dentro del proyecto.

### 1.1. Glosario

<!-- ![Glosario](/profile/assets/glosario.png) -->

| Término                  | Definición                                                                      |
| ------------------------ | ------------------------------------------------------------------------------- |
| Producto Cinematográfico | Una película, serie, o corto                                                    |
| Entrada                  | La publicación con la información de un producto cinematográfico como su reseña |
| Integrantes de Producto  | Actores, directores, guionistas                                                 |
| Calificación             | Es un promedio de 0 a 5 representado con claquetas de cine                      |
| Valorar                  | Dar una calificación a una entrada que puede estar acompañada de una opinión    |

### 1.2. Requerimientos de usuario

Este proyecto será una página web a la que cualquier persona con acceso a internet pueda ingresar, tenemos en mente un flujo de uso principal: el de usuario. Este pdrá buscar y acceder a entradas para ver su información general, sus integrantes y las opiniones de otros usuarios; También podrá crearse una cuenta, lo que le permitirá valorar entradas e interactuar con otras valoraciones a través de un botón de 'me gusta' y comentarios.

## 2. Requerimientos de Sistema

### 2.1. Arquitectura de sistema

Como mencionamos en la introducción del documento el sistema está centrado en una base de datos, pues el objetivo primordial del proyecto es almacenar información, principalmente valoraciones de usuarios, sobre la mayor cantidad de productos cinematográficos y mostrarlos al mundo cinéfilo. Con lo anterior también denotamos que una parte importante del sistema de igual manera es el mostar la información, por lo que queremos brindar una interfaz gráfica llamativa y de esta manera alcanzar e impactar a la mayor cantidad de usuarios.

Tendremos un desarrollo independiente de las diferentes partes de nuestro sistema las cuales son: una página de internet que este basada en las tecnologías principales del desarrollo frontend, una base de datos que almacene la toda la información necesaria para el proyecto, además de permitirnos hacer consultas de manera rápida y una infrastuctura que nos permita: recibir consultas por parte de la página en internet, realizar las consultas en la base de datos, validar los cambios en la base e identificar a los usuarios, por mencionar algunas de las acciones más importantes. 

A manera de resumen la arquitectura que usaremos para el proyecto será la arquitectura de tres niveles:

1. Nivel de presentación: la interfaz de usuario
2. Nivel de aplicacón: la parte lógica 
3. Nivel de datos: la base de datos

## 3. Especificaciones

### 3.1. Registro de cuenta

**Motivo:** Crea un espacio en la base de datos donde se guardará información que es distinta para cada usuario que quiera tener acceso a las funcionalidades completas de la plataforma.

**Flujo:** Una vez dado clic en “registrarse”, se desplegará un formulario para obtener la siguiente información.

- Nombre de usuario
- Nombre completo (Nombre y apellido por separado)
- Correo electrónico
- Contraseña y confirmación
- Fecha de nacimiento (Día, mes y año)
- País de origen

Esta información se pasa por un validador y después al controlador. (Se creará la instancia en la base de datos) y se enviará un correo para verificar la cuenta con un token de duración (48hrs) una vez pasado el tiempo se eliminará la información obtenida. Para registrarse se repetirá el proceso.

**Notas adicionales:**

- El correo no debe estar siendo ocupado por otro usuario.
- Las contraseñas deben coincidir.

### 3.2. Inicio de sesión

**Motivo:** Acceso a información especifica del usuario y a funcionalidades de la plataforma.

**Flujo:** Una vez dado clic en “iniciar sesión” se desplegará un formulario pidiendo

- Correo electrónico
- Contraseña

Se enviará la información al validador y después al controlador, una vez obtenida una respuesta de aceptación se regresará a la pantalla principal de la plataforma con las funcionalidades ya desbloqueadas y acceso a su perfil.

**Notas adicionales:**

- El correo debe estar confirmado.
- La contraseña debe ser valida.

### 3.3. Búsqueda de entradas

**Motivo:**  Conocer información de interés para el usuario

**Flujo:** El usuario podrá buscar la información de una entrada mediante una barra de búsqueda que se encontrará en la parte superior.

### 3.4. Valorar una entrada

**Motivo:** Calificar alguna entrada, con la opción de dejar un comentario que respalde dicha calificación.

**Flujo:** Para cada entrada en particular que no haya sido valorada antes habra un campo para dar un calificación en claquetas y un campo opcional para agregar el comentario/opinión, depues de dar la calificación se activa el botón “calificar”. Al darle clic a este, la opinión se carga en la base y aparece con el resto de opiniones de la entrada para que los demás usuarios puedan interacutar con ella. El campo para calificar es sustitudo por la calificación que se agregó. 

### 3.5. Responder una valoración

Nota: Esto incluye darle like o dislike a una valoración

**Motivo:** Empezar a una conversación a raiz de la valoración de otro usuario sobre un producto cinematográfico 

**Flujo:** Entramos a una entrada, bajamos a ver las opiniones de los usuarios, habrá varios logos: un like, un dislike y un comentario. Si se da click al like o dislike se mostarará la gráfica de aceptación que lleva la opinión al momento. Al dar click en el comentario aparecera un area para meter texto con un boton de comentar en la parte inferior, al apretar el botón comentar se mostrará el comentario indexado en la opinion que replico. 

**Notas adicionales:**

- Solo los usuarios con una cuenta pueden realizar estas acciones

## 4. Gráficas

### 4.1. Modelo Relacional

![ModeloRelacional](/profile/assets/relacional.png)

### 4.2. Flujo de Usuario

![FlujoUsuario](/profile/assets/flujo-usuario.png)

## 5. Mockup

[CineForum](https://xd.adobe.com/view/dcd80ca7-0092-41ca-b9f6-d428f85ce852-898b/screen/6781ac7d-5ce0-465c-a128-cb587962e0c7?fullscreen)

## 6. Apéndice

Se enlistan a continuación las opiniones y conclusiones finales de cada integrante del equipo.

- **Leslie Ramírez Gallegos**

Aunque hubo funcionalidades que no pudimos mostrar al usuario final me siento bien con el resultado del sistema pues cumple con la finalidad que es manipular las entradas y tal. Posiblemente el backend se pueda mejorar al igual que el frontend. Hablando desde la posición de estudiante; lo que me llevo del semestre es haber mejorado la habilidad de aprender tecnologías que estan en el mercado, hacer análisis de mercado para lanzar una app que pueda tener crecimiento. Del lado de software; la importancia de las pruebas en código, entender los requisitos del cliente, etc. 

- **uriel**

  texto
  
- **Fernando Márquez Pérez**

  En lo personal me encuentro satisfecho con el resultado final pues, a pesar de todo lo que terminamos no agregando, presentamos algo íntegro, funcional y con un diseño similar al planeado al inicio. Pero considero que, junto con errores de estimación en el tiempo y la complejidad de desarrollo de algunas funcionalidades que inicialmente creíamos serían sencillas, tuvimos problemas en la comunicación y organización como **equipo** que nos impideron cumplir con las expectativas que teníamos para el proyecto, y es que, al menos por mi parte, había periodos en los que no sabía nada de los avances de mis compañeros y, a raíz de no conocerlos de antes, tampoco mostraba el interes que debía para preguntarles como iban o si podía ayudar en algo y me limitaba a hacer *"lo que me tocaba"*. 

- **fer garay**

  texto

- **fer lopez**

  texto
