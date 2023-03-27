#  ng-scroll

Subir un scroll con un boton en Angular usando JQuery

## Dependencias

### Angular material 

Para instalar Angular Material para angular cli en su proyecto ejecute el siguiente comando: 

```bash
ng add @angular/material
```

### JQuery
Para instalar JQuery en su proyecto siga los siguientes pasos:

* Ejecute el siguiente comando en una terminal de su proyecto.

```bash
npm install jquery — save
```


* En el archivo Angular.json agrege en la propiedad scripts la siguiente linea:

```json
"scripts": [
              "node_modules/jquery/dist/jquery.min.js"
            ]
```

* En el componente que vaya a usar JQuery declare

```typescript
declare var $: any;
```


##  Crear boton flotante 

### html 

En el archivo .html de su componente donde desea utilizar el boton agregue:

```html
<button *ngIf="showGoUpButton" mat-mini-fab class="button_up_content" (click)="contentUp()">
    <mat-icon>arrow_upward</mat-icon>
</button>
```

### css

En el archivo .css de su componente donde desea utilizar el boton agregue:

```css

/*Boton ir arriba*/
.button_up_content {
    position: fixed;
    z-index: 1000;
    bottom: 75px;
    right: 60px;
    font-size: 20px;
  }
  
  @media screen and (max-width: 992px) {
    .button_up_content {
      bottom: 75px;
      right: 30px;
      font-size: 20px;
    }
  }

/*Fin Boton ir arriba*/
```

### ts

En el archivo .ts de su componente donde desea utilizar el boton agregue:
 
* Declare las variables

  ```typescript
  //Subir contenido
  showGoUpButton = false;
  //En cunatos pixeles se va a mmostrar el boton 
  showScrollHeight = 400;
  //en cuantos se va a ocultar
  hideScrollHeight = 200;
  ```

* Crear evento 

  ```typescript
  //Ecuchando scroll en todos los elementos
  scrollEvent = (event: any): void => {
    const number = event.srcElement.scrollTop; //Donde inicia el scroll

    //verificar que el scrool se ejecute dentro de la calse container_main
    if (event.srcElement.className == "container_main") {
      //evakuar si el scroll esta en la cantidad de pixeles para mostrar el boton 
      if (number > this.showScrollHeight) {
        this.showGoUpButton = true; //MMostatr boton
      } else if (number < this.hideScrollHeight) {
        this.showGoUpButton = false; //ocultar boton 
      }
    }
  
  }
  ```

* En el constructor agregar el evento:

```typescript
constructor(
  ) {
      //agregar evento
    window.addEventListener('scroll', this.scrollEvent, true);
  }
```
 
* Agregar ngOnDestroy para parar el evento fuera de la ventana

```typescript
ngOnDestroy() {
    window.removeEventListener('scroll', this.scrollEvent, true);
  }

```

* Cree la funcion del boton 

```typescript
//Funcion para subir contenido
  contentUp() {
    $('.container_main').animate({ scrollTop: (0) }, 2000);

  }
```

  
