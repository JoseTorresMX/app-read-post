# Leer post
App de desarrollada en Angular, con el proposito de consumir APIRest tipo *mock*, tiene una estructura sencilla, solo consume la API y muestra un listado.
![Codigo funcionando y mostranto listado de publicaciones](img/image.png)

# Crear proyecto
```
ng new <nombre_proyecto> --standalone=false
```
Creamos el componente y un servicio
```
ng generate component post
```
```
ng generate service post
```
# Configuramos el servicio
Vamos a consumir una [API JSON](https://jsonplaceholder.typicode.com/posts). Abrimos el archivo **post.service.ts** y lo configuramos:
```
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';
@Injectable({
 providedIn: 'root'
})
export class PostService {
 private apiUrl = 
 'https://jsonplaceholder.typicode.com/posts';
 constructor(private http: HttpClient) {}
 getPosts(): Observable<any> {
 return this.http.get(this.apiUrl);
 }
}
```
# Configuramos el componente para mostrar las publicaciones
Vamos al archivo **post.component.ts** y le damos una ligera modificada para obtener y mostrar los datos consumidos:
```
import { Component, OnInit } from '@angular/core';
import { PostService } from '../post.service';
@Component({
 selector: 'app-post',
 templateUrl: './post.component.html',
 styleUrls: ['./post.component.css']
})
export class PostComponent implements OnInit {
 posts: any[] = [];
 constructor(private postService: PostService) {}
 ngOnInit() {
 this.postService.getPosts().subscribe((data: any) => {
 this.posts = data; // Guarda la lista de publicaciones en la variable
 });
 }
}
```
# Creamos la interfaz del usuario
Vamos al archivo **post.component.html** y le agregamos el diseño que necesitamos para mostrar la lista de publicaciones:
```
<div style="text-align: center;">
 <h2>Lista de Publicaciones</h2>
 <ul>
 <li *ngFor="let post of posts">
 <h3>{{ post.title }}</h3>
 <p>{{ post.body }}</p>
 </li>
 </ul>
</div>
```
**Nota**:Se usa *ngFor* para iterar sobre cada publicacion en la lista *post* y mostrar el *title* y *body*.

# Importamos el modulo HttpClientModulo
Vamos al modulo de la aplicacion el cual es **app.module.ts** e importamos el modulo mencionado:
```
import { NgModule } from '@angular/core';
import { BrowserModule, provideClientHydration } from '@angular/platform-browser';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { PostComponent } from './post/post.component';

// Importar el modulo para HTTTP
import { HttpClientModule } from '@angular/common/http';

@NgModule({
  declarations: [
    AppComponent,
    PostComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    HttpClientModule //Importamos para las solicitudes HTTP
  ],
  providers: [
    provideClientHydration()
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
# Incluir el componente en la vista principal
Vamos al archivo **app.component.html** e incluimos el selector *<app-post>* para que el componente se muestre.
```
<!-- app.component.html --> <app-post></app-post>
```
# Lanzamos la aplicacion
En la terminal:
```
ng serve
```
Nos dara una URL con el servidor de desarrollo **http://localhost:4200/**, lo copiamos y lo pegamos en la barra de direcciones de nuestro navegador.
