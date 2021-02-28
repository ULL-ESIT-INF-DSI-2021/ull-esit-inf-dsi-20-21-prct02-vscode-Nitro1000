# ull-esit-inf-dsi-20-21-prct02-vscode-Nitro1000
<h1><a id="user-content-práctica-2-instalación-y-configuración-de-visual-studio-code" class="anchor" aria-hidden="true" href="#práctica-2-instalación-y-configuración-de-visual-studio-code"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a>Práctica 2: Instalación y configuración de Visual Studio Code</h1>

## Índice
1. [Introducción](#id1)
2. [Instalación y funcionalidad de Visual Studio Code](#id2)
3. [Configuración de Visual Studio Code para conectarse a una máquina remota por SSH](#id3)
4. [Primer proyecto en TypeScript: “Hola Mundo”](#id4)

## Introducción<a name="id1"></a>

<p>En esta segunda practica tendremos que instalar y configurar <a href="https://es.wikipedia.org/wiki/Visual_Studio_Code" rel="nofollow">Visual Studio Code</a> que es un editor de texto desarrollado por Microsoft para distintos sistemas operativos y con soporte para diferentes tareas para desarrolladores como debugging o control de versiones con Git. Además, lo configuraremos de tal manera que nos permita trabajar desde la maquina local en la maquina virtual del IaaS gracias a los plugins.</p>

### Instalación y funcionalidad de Visual Studio Code<a name="id2"></a>

<p>Lo primero que deberemos hacer será instalar VScode en nuestra máquina local. En la local se puede hacer de varias maneras, por ejemplo: linea de comandos, desde la pagina oficial de VScode, desde la tienda de aplicaciones de la distro linux que tengamos, etc. En este caso se hara por linea de comandos en Ubuntu:</p>
<code>
$ sudo apt install code
[sudo] contraseña para usuario: 
Leyendo lista de paquetes... Hecho
Creando árbol de dependencias       
Leyendo la información de estado... Hecho
No hay un paquete apt "code", pero hay un snap con ese nombre.
Intente «snap install code»
E: No se ha podido localizar el paquete code
</code>

<p>Si ocurre este error de no localizar el paquete, podemos probar con snap. El comando seria el siguiente:</p>
<code> $ sudo snap install code --classic</code>

  
### Configuración de Visual Studio Code para conectarse a una máquina remota por SSH<a name="id3"></a>

<p>Tenemos que poder conectarnos desde VScode a nuestra maquina virtual mediante una extencion llamada <a href="https://code.visualstudio.com/docs/remote/ssh-tutorial" rel="nofollow">Remote - SSH</a>. Para instalarla podemos buscarla en el apartado de extenciones/plugins en el lateral izquierdo de la aplicación.</p>
![Icono de Remote-SSH](https://code.visualstudio.com/assets/docs/remote/ssh-tutorial/remote-ssh-extension.png)
<p>Ya instalada la extención nos conectamos a la VPN de la ULL (en caso de no estar en la red universitaria), ahora precionamos <code>F1</code> y escribimos <code>ssh</code>, nos aparece la opción <code>SSH-Remote: Connect to host</code> en el caso de que no aparezca el nombre de la maquina virtual, tenemos que acceder al fichero <code>~/.ssh/config</code> y agregar lo siguiente:</p>

<code>
Host iaas-dsi2
  HostName iaas-dsi2
  User usuario
</code>

<p>Una vez hecho esto, nos aparecera la maquina virtual y nos podremos conectar por ssh.</p>
  
### Primer proyecto en TypeScript: “Hola Mundo”<a name="id4"></a>

<p>Tendremos que instalar otras extenciones que son las siguientes:
 <p>1. ESLint que permite realizar comprobaciones de estilo sobre ficheros que incluyan código fuente en JavaScript y TypeScript.</p>
 <p>2. Live Share permite colaborar en las tareas de desarrollo en tiempo real.</p>
 Ahora, lo que haremos será instalar el compilador de TypeScript. Para ello, usaremos npm:
</p> 

<code>
$npm install --global typescript
added 1 package, and audited 2 packages in 5s
found 0 vulnerabilities
</code>


<p>Ahora podemos empezar a desarrollar el primer proyecto, haremos lo siguiente:</p>

<code>
$mkdir hello-world
$cd hello-world/
$npm init --yes
Wrote to /home/usuario/hello-world/package.json:

{
  "name": "hello-world",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
</code>

<p>El comando <code class="language-bash highlighter-rouge">npm init --yes</code> permite crear un fichero denominado <code class="language-bash highlighter-rouge">package.json</code>, el cual se utiliza, entre otras cosas,
para establecer las dependencias de desarrollo y ejecución del proyecto a modo de paquetes de los que depende el
proyecto actual.</p>
<p>Si queremos podemos usar para los siguientes pasos el VScode que nos facilita la edición y la visualización del código.</p>
<p>Añadimos el directorio a un espacio de trabajo (<em>workspace</em>). Para ello, vamos al menú <code class="language-bash highlighter-rouge">File</code> y seleccione
la opción <code class="language-bash highlighter-rouge">Add Folder to Workspace...</code>. Seleccione <code class="language-bash highlighter-rouge">hello-world</code> en el menú desplegable. Si no tenía un espacio de trabajo creado previamente, se creará uno nuevo y se añadirá el directorio al mismo. Guarde el espacio de trabajo seleccionando la opción <code class="language-bash highlighter-rouge">Save Workspace As...</code> del menú <code class="language-plaintext highlighter-rouge">File</code>, escriba un nombre de fichero y pulse el botón <code class="language-bash highlighter-rouge">OK</code>.</p>
<p>Dentro del directorio hello_world se crea un fichero llamado tsconfig.json al que le añadiremos lo siguiente:</p>

<code>
{
  "compilerOptions": {
    "target": "ES2018",
    "outDir": "./dist",
    "rootDir": "./src",
    "module": "CommonJS"
  }
}
</code>

<p>target: Es para generar código compatible con uno de los últimos estándares de JavaScript. outDir: El código JavaScript producto de la compilación se almacenará en un directorio <code class="language-plaintext highlighter-rouge">dist</code>. rootDir: Especificamos que el código fuente escrito en TypeScript se encuentra en el directorio <code class="language-plaintext highlighter-rouge">src</code>. module: Se indica un estándar para cargar código desde ficheros independientes.</p>
<p>Ahora, añadiremos un fichero con código TypeScript. Ejecute los siguientes comandos en la terminal de VSCode en la carpeta hello-world:</p>
<div class="language-bash highlighter-rouge">
<div class="highlight">
<code>
$mkdir src
$cd src
$touch index.ts
</code>
</div></div>
<p>Para realizar nuestro primer <em>hola mundo</em>, primero debemos escribir las siguientes líneas de código en el fichero que acabamos de crear,guardamos y podemos ejecutarlo con <code>tsc</code>.</p>

<code>
let myString: string = "Hola Mundo";
console.log(myString);
</code>

<p>Se crea automáticamente el directorio dist y un fichero llamado index.js. Vemos las diferencias que tienen:</p>

<code>
$diff src/index.ts dist/index.js 
1c1
< let myString: string = "Hola Mundo";
---
> let myString = "Hola Mundo";
</code>

<p>La diferencia se encuentra en la declaración de la variable myString. Una de las principales funcionalidades de TypeScript es que utiliza tipos para tratar de evitar los problemas que surgen con JavaScript, el cual no es un lenguaje tipado.</p>
<p>Ejecutamos el codigo JS generado a partir del código TypeScript mediante el siguiente comando:</p>

<code>
$node dist/index.js
Hola Mundo
</code>

