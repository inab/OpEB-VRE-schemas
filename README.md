## How to connect the Project

**Web:** https://dev2-openebench.bsc.es/

Login (para hacer pruebas → test):
* **Username:** test@bsc.es
* **Password:** -

**Abrir la VM en Visual Studio en tu ordenador:**
* ```sh
   ssh -f -N -L 2249:10.32.1.249:22 user@oeb-login.bsc.es
   ```
* ```sh
   sshfs -o port=2249 user@localhost:/home/CARPETA_EN_LOCAL
   ```
* Una vez tenemos esto en local, accedemos a la carpeta https://github.com/inab/openEbench-frontend/tree/development/src/app y tenemos todos los componentes.

**Para hacer build y que se vea todo en la web:** 
```sh
npm run build-raw -- --optimization=false
```
![image](https://user-images.githubusercontent.com/51945891/133595485-0d73ea97-2157-472e-9588-d8591ccf0c2e.png)
      
## Apartado Usuario → New Benchmarking Event
Crea un formulario a partir de unos JSON Schemas para crear un nuevo benchmarking event (todo automático).

![image](https://user-images.githubusercontent.com/51945891/133595611-1df11f14-a890-4cac-9ced-987f71181a4a.png)

### Donde están los JSON Schemas?
https://github.com/inab/OpEB-VRE-schemas/tree/frontend-schema

https://github.com/inab/OpEB-VRE-schemas/tree/frontend-mode-schema
Estos segundos schemas se necesitan para que el formulario se cree correctamente ya que tiene muchas $ref a otros ficheros. José María hizo un parser para que funcionara correctamente. Este parser necesita esta estructura entre schemas. 

### Que librería se usa para el formulario? 
https://formly.dev/

https://formly.dev/examples/advanced/json-schema → ejemplos de JSON Schemas con formulario y la librería correspondiente.

El formulario crea todo menos los selects con información de la API.

### Donde está el código en el que se crea el formulario? 
https://github.com/inab/openEbench-frontend/tree/development/src/app/BDMCreator
El código está comentado.

El formulario tiene types. Es decir, si el schema tiene que X elemento es type=object, este tiene una estructura concreta; con array lo mismo, etc. Estos types están en https://github.com/inab/openEbench-frontend/tree/development/src/app/BDMCreator/schema-types

### Donde se crea el select y el botón new? 
https://github.com/inab/openEbench-frontend/tree/development/src/app/BDMCreator/schema-types/BDMLoader


### BDMLoader:
* Como sabe el formulario que tiene que aparecer un select? Para que aparezca un select en medio del formulario es con type=BDMLoader dentro del apartado widget y formlyConfig, como en la siguiente imagen:

![image](https://user-images.githubusercontent.com/51945891/133595573-4aaeec34-68dd-46b0-84ce-87e457b728c5.png)

#### templateOptions de BDMLoader (JSON Schema):
1. **short_name:** Ha de ser igual al nombre correspondiente que tenga el archivo de https://github.com/inab/OpEB-VRE-schemas/tree/frontend-mode-schema
2. **title:** Titulo que quiero que aparezca al abrir el formulario correspondiente (si tiene new button).
3. **BDMType:** Ha de coincidir con el nombre de ese atributo, en este caso es community_id.
4. **multiple:** Si quiero que el select sea de tipo multiple o solo una única opción.
5. **new_button:** Si es = true, existe un botón “New” para poder crear un elemento de ese tipo. Si es = false o simplemente no existe, no crea ese botón.
6. **url_select:** Sirve para coger la información haciendo un GET a la API, es la URL que usará. Pueden haber objetos que puedan tener información tanto en staged como en sandbox. “url_select” permite que dentro haya tanto staged cómo sandbox, si alguno de los dos no está, simplemente no los lee. 
   1. **url_staged:** Si es de la base de datos staged.
   2. **url_sandbox:** Si es de la base de datos sandbox.

## Apartado Usuario → Show sandbox
Aparece una tabla con la información de los elementos que están en la base de datos sandbox.

![image](https://user-images.githubusercontent.com/51945891/133595633-6e62b630-aa7d-4155-834a-ac26a6638084.png)

### Donde está el código? 
En https://github.com/inab/openEbench-frontend/tree/development/src/app/sandbox-selector
