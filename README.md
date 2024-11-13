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

