# Proyecto de cartelera 
En este proyecto se desarrollóun sitio web en el cual se realizó el consumo de una API de usuarios para poder realizar un logueo y tambien una API de peliculas las cuales se muestran como cartelera.
## Servicio para conectar con la API
Primeramente se tiene que los metodos de setItem() y getItem() los cuales ayudaran a poder guardar y recuperar al usuarios que se loguee para que con base a esto se pueda recuperar su nombre de usuario y la foto de perfil que este mismo tenga.
![image](https://github.com/user-attachments/assets/76f091bb-00d6-45d1-a33e-97d9870c5f22)

Tambien se tiene el método de getUsers() con el cual se realiza la consulta a la API de usuarios y nos regresa un observable, esto será necesario en el loguin para poder buscar si existe el usuario ingresado.
![image](https://github.com/user-attachments/assets/cccd51bc-a08d-4e8e-b775-4b7a6ec07310)

Finalmente se tiene el método getSeries() el cual sirve para realizar la consulta con la API de las peliculas este método es un poco distinto al de los usuarios debido a que esta API necesita de headers para poder tener los permisos para recuperar los datos de la API para ello se debe incluir los datos que proporciona la misma API e importar el HttpHeaders.
![image](https://github.com/user-attachments/assets/82d98a09-9ae4-4def-9e21-8c084989d622)

## Login
### ngOnInit()
Este método realiza la recuperacion del observable de los usuarios y lo almacena en la variable usuarios debido a que se utilizará al momento de ingresar y verificar al usuario.
![image](https://github.com/user-attachments/assets/470512e4-7524-4285-9f38-bfdc9026c9ca)

### validar()
Con este método unicamente se valida que no hayan campos vacios dentro del login y muestra un mat-error en caso de que así sea.
![image](https://github.com/user-attachments/assets/b4272ab1-42ae-4de5-b4d2-168b09bed9bb)

### ingresar()
Para poder ingresar primero se valida que los campos de correo y contraseña no estén vacíos, una vez verificado se procede a buscar en el arreglo de usuarios si coincide algun usuario con el correo y la contraseña ingresada, se ser así se guarda ese usuario en el localstorage y se redirecciona al home del sitio, sino se encuentra alguna coincidencia se manda el error de las credenciales.
![image](https://github.com/user-attachments/assets/e81c2bac-789d-4b80-9602-ab962e90e3d5)

## Home
### ngOnInit()
Se realiza la consulta de las pelicula que nos retorna el servicio para poder guardarlos en los datos de la tabla, pero conforme se van recuperando las pelicula se les agrega un nuevo campo incrementable que es un contador para poder llevar una numeración de las pelicula que se ingresan. Tambien se realiza la recuperacion del localstorage del usuario para poder usar el avatar y su nombre en la pantalla.
![image](https://github.com/user-attachments/assets/56e7255e-b7ef-4d76-8a5e-cb3b49990546)

### ngAfterViewInit() 
Este método ayuda a esperara que una vez que ya se tienen los datos en la tabla y se han aplicado puesto que es necesario que ya esten los datos para poder aplicar los filtros y la paginacion de los elementos.
![image](https://github.com/user-attachments/assets/890809a6-4ea6-4573-a65c-1fed7bc292a2)

### openVer()
Se ejecuta la ventana modal de ver a la cual se le envia la pelicula seleccionada y el titulo que llevará la ventana modal, debido a que solamente es para ver los datos no se maneja ninguna accion para cuando la ventana se cierra.
![image](https://github.com/user-attachments/assets/9a0ed757-749b-48f6-9350-466f0ebe4984)

### openEditar()
Se manda a ejecutar la ventana modal, enviando la pelicula que se seleccionó en la tabla y el titulo de la ventana, una vez que el usuario cierre la ventana se procede a manejar los cambios como se recibe la pelicula con o sin los cambios realizados este mismo se asigna en la posicion donde se encuentra la pelicula con los datos anteriores, posteriormente se notifica que hbieron cambios en la tabla para que esta misma sea actualizada.
![image](https://github.com/user-attachments/assets/f355d860-4840-4eb1-836e-0d9df0ce95e1)

### openEliminar()
Se ejecuta la ventana modal y se envia la pelicula seleccionada para que se pueda mostrar el titulo de la pelicula que se va a eliminar; una vez que el usuarios cierre la ventana si se cancelo la eliminación no se recibe nada entonces no se realiza ninguna acción por otra parte si se recibe el id de la pelicula se manda a llamar al metodo eliminar el cual se encarga de eliminar la pelicula y actualizar la tabla.
![image](https://github.com/user-attachments/assets/ea290dfb-5cc2-4f5f-9daa-5ad20dce9655)

### eliminar()
En este método primero se realiza la busqueda del indice en el que se encuentra la pelicula con la que se está trabajando, una vez encontrado en indice se corta de los datos de la tabla y a todos los elementos que esten posterior a ese indice se les reduce su contador para mantener una consistencia en los contadores, finalmente se notifica y actualiza la tabla.
![image](https://github.com/user-attachments/assets/9aa145a8-16ab-4e4a-9dc4-f4b0207eac01)

### applyFilter()
Con este método se realiza la busqueda de lo que el usuario necesite por ello se recupera lo que se está ingresando por el usuario y se filtra dentro de los datos de la tabla.
![image](https://github.com/user-attachments/assets/96aa5b2e-0691-483c-902a-91fc030c46b8)

### handleError()
Este método es para manejar el error que si existe alguna imagen que no pueda ser cargada o dañada del avatar del usuario, se coloque una imagen provisional para indicar que no se ha encontrado.
![image](https://github.com/user-attachments/assets/8983a6c8-7a4d-4a26-af5b-d0311f7e65d4)

## Editar
Se cuenta con dos métodos uno que es el de cerrar el cual se cierra sin realizar ningun cambio a la película y esto hará que en la vetana principal no se realicen cambios a la tabla.
![image](https://github.com/user-attachments/assets/89917eae-0096-42a1-ae3e-3e360eead80f)

Tambien se tiene el método guardar, el cual cierra la ventana modal pero al mismo tiempo envia la variable pelicula la cual puede o no tener cambios puesto que esta se sustituirá en la tabla princopal con lo que haya hecho el usuario.
![image](https://github.com/user-attachments/assets/fe891f8a-51cf-4bf4-b897-b02fa42669a9)

Se cuenta con un método de validar para asegurar que los campos editables del formulario contengan al menos un caracter, esto se aplica para todos excepto el id debido a quees un campo que se muestra pero no puede ser modificado, si algún campo se deja en blanco se marcará un mat-alert para notificar el error.
![image](https://github.com/user-attachments/assets/02c4c10b-80ba-4eb0-a46a-5dd40edf1b5e)

## Ver
Debido a que esta ventana modal solamente muestra los datos de la pelicula no cuenta con muchos métodos solo el de cerrar el cual no retorna ningun valor que se vaya a manejar en la ventana del home.
![image](https://github.com/user-attachments/assets/14584b13-2927-48aa-9811-c3d0e63f593f)

## Eliminar
Se tienen dos métodos en la ventana de eliminar debido a que si el usuario selecciona cancelar,  la ventana se cierra sin devolver ningun valor y como se explicó en el openEliminar() sino se recibe ningun valor no se aplica ninguna acción, por otra parte si el usuario acepta eliminar es cuando se cierra la ventana pero se envía el id de la pelicula que se desea eliminar para que de esta manera se ejecute la eliminación.
![image](https://github.com/user-attachments/assets/244f30ff-efbf-44fe-a307-3615985e4986)

## Ejecución
### Login
Para la ejecución del login se utilizó al usuario administrador que con aterioridad se verificó que existiera dentro de la API al dar clic en inicar sesion nos redirecciona al home.
![image](https://github.com/user-attachments/assets/c014ab8c-94f1-452b-80dc-abafd29ca92c)

### Home
Dentro del home se puede apreciar los datos de la sesión teniendo la foto de perfil y el nombre, tambien se puede apreciar la tabla de las peliculas con los campos principales y las acciones que puede realizar el usuario.
![image](https://github.com/user-attachments/assets/bbb3cfba-644b-423a-86dc-bb9d45fc43fb)

### Modal Ver
Al desplegar la ventana modal de ver se muestran más datos de la pelicula como el género, año que se lanzó, descripcion y tipo de filmación
![image](https://github.com/user-attachments/assets/92c4e324-37f9-438a-9b30-e4ccd3803874)

### Modal Editar
En la ventana de esitar se muestran todos los campos que podremos editar, a excepcion del ID que se muestra pero no puede ser modificado en este caso la pelicula de ghost se cambiará el titulo a cambio hecho y se puede ver el cambio realizado al titulo.
![image](https://github.com/user-attachments/assets/53bebe9d-cd99-47aa-8c92-5df9fa9ff7f3)

![image](https://github.com/user-attachments/assets/8a2db0ff-f869-4a2d-83fc-ef95b70e3398)

### Modal Eliminar
Finalmente se eliminará la pelicula con el cambio realizado y se puede ver como la columna id que es el contador se actualiza y la pelicula ya no es mostrada.
![image](https://github.com/user-attachments/assets/3eefd91a-ba8e-4cc1-aad7-7b92483dc305)

![image](https://github.com/user-attachments/assets/9b86005d-9f01-4a30-ac9c-da7adf85889c)



## Proyecto
This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 18.2.11.

## Development server
Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The application will automatically reload if you change any of the source files.

## Code scaffolding
Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build
Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory.

## Running unit tests
Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests
Run `ng e2e` to execute the end-to-end tests via a platform of your choice. To use this command, you need to first add a package that implements end-to-end testing capabilities.

## Further help
To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI Overview and Command Reference](https://angular.dev/tools/cli) page.
