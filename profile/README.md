# Requerimientos de Sistema

## Índice

- [Introducción](#introduccion)
    - [Glosario](#glosario)
    - [Requerimientos de Sistema](#req-usuario)
- [Requerimientos de Sistema](#req-sistema)
    - [Arquitectura del Sistema](#arq-sistema)
- [Especificaciones](#especificaciones)
    - [Registro de cuenta](#registro-cuenta)
    - [Inicio de sesión](#inicio-sesion)
    - [Búsqueda de entradas](#busqueda-entradas)
    - [Valorar una entrada](#valorar-entrada)
    - [Responder una valoración](#responder-valoracion)
- [Gráficas](#graficas)
    - [Modelo Relacional](#relacional)
    - [Flujo de Usuario](#flujo-usuario)
- [Mockup](#mockup)
    

## 1. Introducción <a name='introduccion'></a>

El propósito de este documento es describir las bases fundamentales, en lo que a requerimientos respecta, sobre los que se desarrollará un foro de discusión centrado en una base de datos orientada al mundo cinematográfico con características típicas de una red social para compartir reseñas y opiniones. 

Bajo esta idea a lo largo del documento abordaremos, en primera instancia, los atributos que queremos encuentre el usuario en nuestra página, tanto de manera directa como las acciones que tendrá a sus disposición y de manera indirecta como el espacio que queremos brindar en la comunidad. Posteriormente veremos los detalles prácticos que se necesitarán para poder realizar el foro como: arquitectura de sistema, flujo de acciones y modelos dentro del proyecto.

### 1.1. Glosario <a name='glosario'></a>

![Glosario](/assets/glosario.png)

### 1.2. Requerimientos de usuario <a name='req-usuario'></a>

Este proyecto será una página web a la que cualquier persona con acceso a internet pueda ingresar, tenemos en mente dos flujos de uso principales: usuario y administrador. Como usuario podemos acceder a entradas y a perfiles de un integrante de producto donde se muestre los productos cinematográficos en los que ha participado; un usuario se puede crear una cuenta con la cual podrá: valorar entradas, comentar valoraciones. Las acciones pensadas para los administradores son, como indica su nombre, administrar el contenido de la página en todas sus formas, siendo estas: todo lo relacionado a entradas e integrantes de un producto.

## 2. Requerimientos de Sistema <a name='req-sistema'></a>

### 2.1. Arquitectura de sistema <a name='arq-sistema'></a>

Como mencionamos en la introducción del documento el sistema está centrado en una base de datos, pues el objetivo primordial del proyecto es almacenar información, principalmente valoraciones de usuarios, sobre la mayor cantidad de productos cinematográficos y mostrarlos al mundo cinéfilo. Con lo anterior también denotamos que una parte importante del sistema de igual manera es el mostar la información, por lo que queremos brindar una interfaz gráfica llamativa y de esta manera alcanzar e impactar a la mayor cantidad de usuarios.

Tendremos un desarrollo independiente de las diferentes partes de nuestro sistema las cuales son: una página de internet que este basada en las tecnologías principales del desarrollo frontend, una base de datos que almacene la toda la información necesaria para el proyecto, además de permitirnos hacer consultas de manera rápida y una infrastuctura que nos permita: recibir consultas por parte de la página en internet, realizar las consultas en la base de datos, validar los cambios en la base e identificar a los usuarios, por mencionar algunas de las acciones más importantes. 

A manera de resumen la arquitectura que usaremos para el proyecto será la arquitectura de tres niveles:

1. Nivel de presentación: la interfaz de usuario
2. Nivel de aplicacón: la parte lógica 
3. Nivel de datos: la base de datos

## 3. Especificaciones <a name='especificaciones'></a>

### 3.1. Registro de cuenta <a name='registro-cuenta'></a>

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

### 3.2. Inicio de sesión <a name='inicio-sesion'></a>

**Motivo:** Acceso a información especifica del usuario y a funcionalidades de la plataforma.

**Flujo:** Una vez dado clic en “iniciar sesión” se desplegará un formulario pidiendo

- Correo electrónico
- Contraseña

Se enviará la información al validador y después al controlador, una vez obtenida una respuesta de aceptación se regresará a la pantalla principal de la plataforma con las funcionalidades ya desbloqueadas y acceso a su perfil.

**Notas adicionales:**

- El correo debe estar confirmado.
- La contraseña debe ser valida.

### 3.3. Búsqueda de entradas <a name='busqueda-entradas'></a>

**Motivo:**  Conocer información de interés para el usuario

**Flujo:** El usuario podrá buscar la información de una entrada mediante una barra de búsqueda que se encontrará en la parte superior.

### 3.4. Valorar una entrada <a name='valorar-entrada'></a>

**Motivo:** Calificar alguna entrada, con la opción de dejar un comentario que respalde dicha calificación.

**Flujo:** Para cada entrada en particular que no haya sido valorada antes habra un campo para dar un calificación en claquetas y un campo opcional para agregar el comentario/opinión, depues de dar la calificación se activa el botón “calificar”. Al darle clic a este, la opinión se carga en la base y aparece con el resto de opiniones de la entrada para que los demás usuarios puedan interacutar con ella. El campo para calificar es sustitudo por la calificación que se agregó. 

### 3.5. Responder una valoración <a name='responder-valoracion'></a>

Nota: Esto incluye darle like o dislike a una valoración

**Motivo:** Empezar a una conversación a raiz de la valoración de otro usuario sobre un producto cinematográfico 

**Flujo:** Entramos a una entrada, bajamos a ver las opiniones de los usuarios, habrá varios logos: un like, un dislike y un comentario. Si se da click al like o dislike se mostarará la gráfica de aceptación que lleva la opinión al momento. Al dar click en el comentario aparecera un area para meter texto con un boton de comentar en la parte inferior, al apretar el botón comentar se mostrará el comentario indexado en la opinion que replico. 

**Notas adicionales:**

- Solo los usuarios con una cuenta pueden realizar estas acciones

## 4. Gráficas <a name='graficas'></a>

### 4.1. Modelo Relacional <a name='relacional'></a>

![ModeloRelacional](/assets/relacional.png)

### 4.2. Flujo de Usuario <a name='flujo-usuario'></a>

![FlujoUsuario](/assets/flujo_usuario.png)

## 5. Mockup <a name='mockup'></a>

[CineForum](https://xd.adobe.com/view/dcd80ca7-0092-41ca-b9f6-d428f85ce852-898b/screen/6781ac7d-5ce0-465c-a128-cb587962e0c7?fullscreen)
