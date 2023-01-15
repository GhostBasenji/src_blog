+++
title = "Поэтапный урок по созданию проекта Angular версии 12"
date = "2021-06-01"
tags = ["Angular"]
+++

В этом уроке мы шаг за шагом пройдем по пути создания проекта Angular с нуля до полноценного приложения, которое использует множество API Angular, таких как HttpClient и Material Design. А также мы будем создадим/смоделируем REST API, и реализуем реальные функции, такие как обработка ошибок и повторная попытка отправки HTTP-запросов в случае неудачи. И наконец, соберем и развернем наш проект в облаке.

<!--more-->

### Список этапов

Этапы этого урока Angular выглядят следующим образом:
- Что узнаем в этом уроке по Angular 12?
- Что будем рассматривать в этом уроке?
- Что такое Angular HttpClient?
- Почему Angular HttpClient?
- Предварительные условия
- Этап 1. Установка Angular CLI v12
- Этап 2. Инициализация нового проекта Angular
- Этап 3. Установка и настройка (Fake) JSON REST API
- Этап 4. Установка Angular HttpClient v9 в наш проект
- Этап 5. Создание компонентов Angular
- Этап 6. Добавление маршрутизации (Routing) в Angular
- Этап 7. Стилизация пользовательского интерфейса с помощью Angular
- Этап 8. Использование JSON REST API с Angular HttpClient
- Этап 9. Добавление обработки ошибок HTTP с помощью RxJS catchError() и HttpClient
- Этап 10. Повторная отправка HTTP-запросов в случае неудачи с помощью RxJS Retry()
- Этап 11. Отмена подписки от HttpClient Observables с помощью RxJS takeUntil()
- Этап 12. Добавление параметров URL-запроса в метод HttpClient get()
- Этап 13. Получение полного HTTP-ответа с помощью Angular HttpClient
- Этап 14. Запрос типизированного HTTP-ответа с помощью Angular HttpClient
- Этап 15. Сборка и развертывание нашего приложения Angular на хостинге Firebase
- Заключение 

### Что узнаем в этом уроке по Angular 12?

* На примере мы узнаем, как отправлять GET-запросы со строками и параметрами URL-запросов и обрабатывать HTTP-ответы с серверов REST API в приложении Angular, используя HttpClient для извлечения и использования данных JSON, как выполнять обработку ошибок для HTTP-ошибок с помощью операторов RxJS throwError() и catchError(), как повторить HTTP-запросы в случае неудачи или при плохих сетевых подключениях, и отменять ожидающие запросы с помощью операторов RxJS retry() и takeUntil().
* А также увидим, как используются службы Angular и RxJS Observables, и узнаем, как устанавливать Angular Material в наш проект и стиль пользовательского интерфейса с компонентами Material Design.
* Узнаем, как использовать функцию ng deploy в Angular для простого развертывания нашего приложения из командной строки на хостинг Firebase.

На данный момент мы используем Angular 12, который имеет новые функции и улучшения, в том числе и новый рендерер Ivy.

***Примечание.*** *Обращаем внимание на то, что тут используется HttpClient, который является улучшенной версией HTTP Client API, доступной начиная с версии Angular 4.3.0-rc.0*.

А также мы можем узнать, как использовать HttpClient с Angular для создания новостного приложения, которое извлекает данные JSON из стороннего REST API, [из этого урока](https://www.techiediaries.com/angular-tutorial-example-rest-api-httpclient-get-ngfor/).

В этом пошаговом уроке Angular 12 мы увидим пример CRUD на практике, и то, как использовать HttpClient, доступный из пакета *@angular/common/http*, как выполнять запросы HTTP GET, используя метод *get()*.

### Что будем рассматривать в этом уроке?
+ Как создается фейковый и полноценный работающий CRUD REST API,
+ Как устанавливается Angular CLI v12,
+ Как создается проект Angular 12 с использованием Angular CLI,
+ Как устанавливаются Angular Material и стиль приложения с помощью Material Design,
+ Как создаются компоненты Angular, маршрутизация и навигация между ними,
+ Как создаются и внедряются службы Angular,
+ Как отправляются HTTP-запросы GET на сервер, используя HttpClient,
+ Как используется класс HttpParams для добавления строк URL-запросов в HttpRequest,
+ Как подписываются на и отписываются от RxJS Observables, возвращаемых HttpClient,
+ Как обрабатываются HTTP-ошибки с помощью операторов throwError() и catchError(),
+ Как повторяются неудачные HTTP-запросы, используя оператора RxJS retry(),
+ Как отписываются от RxJS Observables, возвращаемых от методов HttpClient, используя оператор takeUntil(), когда запросы отменены,
+ Как собрать приложение к производству и развернуть его на хостинге Firebase с помощью команды ng deploy.

Давайте начнем с введения в Angular HttpClient, его возможностей и причин его использования.

### Что такое Angular HttpClient?

Фронт-энд приложения, построенные с использованием таких фреймворков, как Angular, обмениваются данными бэкенд-серверами через REST API (основанные на протоколе HTTP), используя либо интерфейс XMLHttpRequest, либо API *fetch()*.
Angular HttpClient использует интерфейс XMLHttpRequest, который поддерживает как современные, так и устаревшие браузеры.
HttpClient доступен из пакета *@angular/common/http* и имеет упрощенный интерфейс API и мощные функции, такие как легкая тестируемость, типизированные объекты запросов и ответов, перехватчики запросов и ответов, реактивные API с RxJS Observables, и оптимизированная обработка ошибок.

### Почему Angular HttpClient?
Встроенная служба HttpClient предоставляет разработчикам Angular множество преимуществ:
* HttpClient упрощает отправку и обработку HTTP-запросов и ответов,
* HttpClient имеет множество встроенных функций для реализации тестовых модулей,
* HttpClient использует RxJS Observables для обработки асинхронных операций вместо промисов (Promises), которые упрощают общие задачи веб-разработки, такие как:
- сокрытие HTTP-запросов,
- наблюдение за ходом прогресса операций загрузки и выгрузки файлов,
- простая обработка ошибок,
- повторная отправка HTTP-ошибок в случае неудачи, и т.д.

А теперь, после введения в HttpClient, давайте приступим к созданию нашего проекта, начиная с предварительных условий, необходимых для успешного завершения урока Angular 12.

### Предварительные условия

Перед началом нам нужно выполнить предварительные условия:
* Базовые знания TypeScript. В частности, знакомство с объектно-ориентированными концепциями, такими как классы TypeScript и декораторы.
* Локальная машина разработки с Node 10+, вместе с установленным NPM 6+. Node нужен для Angular CLI, как и большинство фронт-энд инструментам в настоящее время. Можем просто перейти на страницу загрузки официального сайта [the official website] и загрузить двоичные файла для нашей ОС.

## Этап 1. Установка Angular CLI v12
Здесь мы установим последнюю версию Angular CLI 12 (на момент написания этого урока).

[Angular CLI](https://angular.io/cli) – официальный инструмент для инициализации и работы с Angular-проектами. Чтобы установить его, открываем командную строку и выполняем следующую команду:

```sh
    npm install -g @angular/cli  
```

На момент написания этого урока angular cli v12 будет установлен в нашей системе.
Если выполнить команду ng version, то увидим:

![](https://i.postimg.cc/nz7tdccV/41.png)

### Этап 2. Инициализация нового проекта Angular

На этом этапе мы перейдем к созданию нашего проекта. Возвращаемся к терминалу и выполним следующую команду:

```sh
  ng new angular-example  
```
CLI задаст нам пару вопросов – **Would you like to add Angular routing?** – Отвечаем да, – и **Which stylesheet format would you like to use?** – выбираем CSS. Этим мы даем команду CLI автоматически настроить маршрутизацию в нашем проекте, поэтому нам нужно будет только добавить маршруты для наших компонентов, чтобы реализовать навигацию в нашем приложении.

Затем переходим в папку проекта и запускаем локальный сервер разработки, используя следующие команды:

```sh
  cd angular-example
  ng serve
```
Это запустит локальный сервер и он соберет проект Angular.

![](https://i.postimg.cc/jSpFtYR1/42.png)

Наше веб-приложение Angular станет доступным по адресу локального сервера: http://localhost:4200/.

![](https://i.postimg.cc/W40f4Y31/43.png)

Оставляем сервер разработки работающим, и открываем новый терминал для выполнения команд следующих этапов.

### Этап 3. Установка и настройка (Fake) JSON REST API

Прежде чем приступить к разработке нашего Angular-проекта, нам нужно подготовить JSON REST API, который можем использовать с помощью HttpClient.

Также мы можем использовать или извлекать данные JSON со сторонних серверов REST API, но в нашем уроке мы решили создать поддельный REST API. Что касается Angular, то нет никакой разницы между использованием поддельных или реальных REST API.

Как уже говорилось, мы можем либо использовать внешнюю службу API, либо создать реальный сервер REST API, либо создать поддельный API с помощью json-сервера. В данном уроке мы будем использовать последний подход.

Итак, перейдем к терминалу и запускаем установку json-server из npm в наш проект:

```sh
  npm install --save json-server
```

Потом создаем папку server в корневой папке нашего Angular-проекта:

```sh
  mkdir server
  cd server
```

В папке server создаем файл *database.json* и добавляем объект JSON:

```json
{
  “products”: []
}
```

Этот файл JSON будет служить базой данных для нашего сервера REST API. Можем просто добавить некоторые данные, которых будут использовать REST API или использовать [Faker.js](https://github.com/marak/Faker.js) для автоматического генерирования большого количества реалистичных поддельных данных.

Возвращаемся в терминал, переходим из папки server выше и устанавливаем *Faker.js* из npm, используя команду:

```sh
  cd .. 
  npm install faker --save 
```

Итак, уже установили faker v4.1.0. А теперь создаем файл generate.js в папке server и напишем следующий код:

```js
var faker = require('faker');

var database = { products: []};

for (var i = 1; i<= 300; i++) {
  database.products.push({
    id: i,
    name: faker.commerce.productName(),
    description: faker.lorem.sentences(),
    price: faker.commerce.price(),
    imageUrl: "https://source.unsplash.com/1600x900/?product",
    quantity: faker.datatype.number()
  });
}
console.log(JSON.stringify(database));
```

Сначала мы импортировали faker, далее определили объект с одним пустым массивов для товаров. Потом мы ввели цикл for, чтобы создать 300 поддельных записей, используя методы, такие как *faker.commerce.productName()* для генерации наименований товаров. В конце мы преобразовали объект базы данных в строку и записали его в стандартный вывод.

Добавляем скрипты **generate** и **server** в файл package.json:

```js
"scripts": {
  "ng": "ng",
  "start": "ng serve",
  "build": "ng build",
  "test": "ng test",
  "lint": "ng lint",
  "e2e": "ng e2e",
  "generate": "node ./server/generate.js > ./server/database.json",
  "server": "json-server --watch ./server/database.json"
},
```

Затем в терминале запускаем скрипт generate, используя следующую команду:

```sh
  npm run generate
```

И потом запускаем сервер REST API, выполнив команду:

```sh
  npm run server
```

Теперь можем отправлять HTTP-запросы на сервер точно также, как и любой типичный сервер REST API. Наш сервер будет доступен по адресу: http://localhost:3000/.

![](https://i.postimg.cc/sg1Dh7dW/44.png)

Имеются конечные точки API, которых мы можем использовать через наш сервер JSON REST API:

* *GET /products* – для получения товаров
* *GET /products/\<id>* – для получения одного товара по идентификатору
* *POST /products* – для создания нового товара
* *PUT /products/\<id>* – для обновления товара по идентификатору
* *PATCH /products/\<id>* – для частичного обновления товара по идентификатору
* *DELETE /products/\<id>* – для удаления товара по идентификатору

Можно использовать параметры _page и _limit для получения данных, разбитых на страницы. В заголовке **Link** мы получаем ссылки first, prev, next и last.

Например:
* **GET /products?_page=1** для получения первой страницы данных
* **GET /products?_page=1&_limit=5** для получения первых пяти товаров первой страницы данных.

Оставляем сервер JSON REST API запущенным и открываем новый терминал.

## Этап 4. Установка Angular HttpClient v9 в наш проект

Здесь мы перейдем к установке модуля HttpClient в наш проект.

HttpClient находится в отдельном модуле Angular, поэтому нам нужно импортировать его в наш основной модуль приложения, прежде чем сможем использовать его.

Открываем наш проект в редакторе кода, в данном уроке я использую Visual Studio Code. Затем открываем файл app.module.ts в папке src/app, импортируем HttpClientModule и добавляем его в массив imports модуля:

```js
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { HttpClientModule } from '@angular/common/http';

@NgModule({
  declarations: [
    AppComponent,
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    HttpClientModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

Вот и все, теперь мы готовы использовать службу HttpClient в нашем проекте, но перед этим нам нужно создать пару компонентов – компоненты home и about. Это то, что будем делать на следующем этапе.

### Этап 5. Создание компонентов Angular
А теперь здесь мы перейдем к созданию компонентов Angular, которые управляют пользовательским интерфейсом нашего приложения.
Выполняем команду в терминале:

```sh
  ng generate component home
```

Вот что у нас получилось:

![](https://i.postimg.cc/vBsWb93J/45.png)

CLI создал 4 файла для компонента и добавил его в массив declarations файла app.module.ts в папке src/app.
Далее создаем компонент about с помощью команды:

```sh
  ng generate component about
```

Открываем файл about.component.html в папке src/app/about и добавляем следующий код:

```html
<p style="padding: 13px;">
    Пример приложения Angular
</p>
```

Мы обновим компонент home в следующих этапах.

### Этап 6. Добавление маршрутизации (Routing) в Angular  

На данном этапе мы научимся добавлять маршрутизацию в наше приложение.

Открываем файл app-routing.module.ts в папке src/app и импортируем компоненты, а потом добавляем маршруты следующим образом:

```js
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';

const routes: Routes = [
  { path: '', redirectTo: 'home', pathMatch: 'full'},
  { path: 'home', component: HomeComponent  },
  { path: 'about', component: AboutComponent  },
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

Сначала мы импортировали компоненты home и about, затем добавили три маршрута, включая маршрут для перенаправления пустого пути к компоненту home, таким образом пользователь, посещая приложение, он будет перенаправлен на домашнюю страницу.

На следующем этапе мы установим и настроим Angular Material в нашем проекте для стилизации пользовательского интерфейса.

### Этап 7. Стилизация пользовательского интерфейса с помощью Angular

На данном этапе мы установим и настроим Angular Material в нашем проекте для стилизации пользовательского интерфейса.

[Angular Material](https://material.angular.io/) предоставляет компоненты Material Design, которые позволяют разработчикам создавать профессиональные пользовательские интерфейсы. Установить и настроить в нашем проекте теперь стало намного проще с помощью команды ***ng add Angular CLI v7+***.

А теперь выполним следующую команду из корневого каталога нашего проекта:
```sh
  ng add @angular/material
```

Нам будет предложено выбрать тему, выбираем **Indigo/Pink**.

Для других вариантов - **Set up global Angular Material typography styles?** и **Set up browser animations for Angular Material?** просто нажимаем клавишу Enter, чтобы выбрать ответы по умолчанию.

Затем открываем файл *styles.css* в папке *src* и добавляем тему:

```js
@import "~@angular/material/prebuilt-themes/indigo-pink.css";
```

Каждый компонент Angular Material имеет отдельный модуль, которого нам нужно импортировать, прежде чем использовать его. Открываем файл *app.module.ts* и добавляем следующие импорты:

```js
import {  MatToolbarModule  } from '@angular/material/toolbar';
import {  MatIconModule } from '@angular/material/icon';
import {  MatCardModule } from '@angular/material/card';
import {  MatButtonModule } from '@angular/material/button';
import {  MatProgressSpinnerModule  } from '@angular/material/progress-spinner';
```

Мы импортировали следующие модули:
- [MatToolbar](https://material.angular.io/components/toolbar/overview) предоставляет контейнер для заголовков, названий или действий.
- [MatCard](https://material.angular.io/components/card/overview) предоставляет контейнер содержимого для текста, фотографий и действий в контексте одной темы.
- [MatButton](https://material.angular.io/components/button/overview) предоставляет собственный элемент ```<button>``` или ```<a>```, улучшенный с помощью стилей Material Design.
- [MatProgressSpinner](https://material.angular.io/components/progress-spinner/overview) предоставляет круговой индикатор прогресса и активности.

Далее мы включаем эти модули в массив *imports*:

```js
@NgModule({
  declarations: [
    AppComponent,
    HomeComponent,
    AboutComponent,
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    HttpClientModule,
    BrowserAnimationsModule,
    MatToolbarModule,
    MatIconModule,
    MatButtonModule,
    MatCardModule,
    MatProgressSpinnerModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

Потом открываем файл *app.component.html* в папке *src/app* и обновляем код:

```html
<mat-toolbar color="primary">
  <h1>
    ngStore
  </h1>
    <button mat-button routerLink="/">Home</button>
    <button mat-button routerLink="/about">About</button>
    </mat-toolbar>
  <router-outlet></router-outlet>
```

Мы создали оболочку нашего приложения, содержащую верхнюю панель с двумя кнопками навигации по компонентам home и about.

### Этап 8. Использование JSON REST API с Angular HttpClient  

На данном этапе мы узнаем, как извлекать данные JSON с нашего сервера REST API, используя HttpClient.

Нам нужно будет создать службу Angular для инкапсуляции кода, которая обрабатывает данные, поступающие с сервера REST API.

Служба – это синглтон, который может быть внедрен в другие службы и компоненты с помощью внедрения зависимостей Angular (Angular dependency injection).

*В программной инженерии внедрение зависимостей – это метод, при котором один объект предоставляет зависимости другого объекта.*

Теперь давайте сгенерируем службу Angular, которая взаимодействует с JSON REST API. В терминале выполним следующую команду:
```sh
  ng generate service data
```

Далее открываем файл *data.service.ts* в папке *src/app*, импортируем и внедряем HttpClient:

```js
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http'; 

@Injectable({
  providedIn: 'root'
})
export class DataService {
    
  private REST_API_SERVER = "http://localhost:3000";

  constructor(private httpClient: HttpClient) { }
}
```

Мы импортировали и внедрили службу HttpClient в качестве приватного экземпляра httpClient. А также определили переменную REST_API_SERVER, которая содержит адрес нашего сервера REST API.

Далее добавляем метод **sendGetRequest()**, который отправляет запрос GET к конечной точке REST API для получения данных JSON:

```js
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http'; 

@Injectable({
  providedIn: 'root'
})
export class DataService {
    
  private REST_API_SERVER = "http://localhost:3000/products";

  constructor(private httpClient: HttpClient) { }

  public sendGetRequest(){
    return this.httpClient.get(this.REST_API_SERVER);
  }
}
```

Этот метод попросту вызывает метод get() объекта HttpClient для отправки запросов GET на сервер REST API.

Теперь нам нужно использовать эту службу в нашем компоненте home. Открываем файл *home.component.ts*, импортируем и внедряем службу данных следующим образом:

```js
import { Component, OnInit } from '@angular/core';
import { DataService } from '../data.service';

@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
export class HomeComponent implements OnInit {

  products = [];

  constructor(private dataService: DataService) { }

  ngOnInit(){
    this.dataService.sendGetRequest().subscribe((data: any[])=>{
      console.log(data);
      this.products = data;
    })
  }
}
```

Мы импортировали и внедрили *DataService* как частного объекта *dataService* с помощью конструктора компонента. Затем мы определили переменную products и вызвали метод *sendGetRequest()* службы для получения данных с сервера JSON REST API.

Так как метод *sendGetRequest()* возвращает возвращаемое значение метода *HttpClient.get()*, который является RxJS Observable, мы подписались на возвращаемый Observable, чтобы фактически отправлять HTTP-запрос GET и обрабатывать HTTP-ответ.

Потом, когда данные получены, добавляем их в массив *products*.

Далее открываем файл *home.component.html* и обновляем его следующим образом:

```html
<div style="padding: 13px;">
    <mat-spinner *ngIf="products.length === 0"></mat-spinner>

    <mat-card *ngFor="let product of products" style="margin-top:10px;">
        <mat-card-header>
            <mat-card-title>{{product.name}}</mat-card-title>
            <mat-card-subtitle>{{product.price}} $/ {{product.quantity}}
            </mat-card-subtitle>
        </mat-card-header>
        <mat-card-content>
            <p>
                {{product.description}}
            </p>
            <img style="height:100%; width: 100%;" src="{{ product.imageUrl }}" />
        </mat-card-content>
        <mat-card-actions>
      <button mat-button> Buy product</button>
    </mat-card-actions>
    </mat-card>
</div>
```

Мы использовали компонент *```<mat-spinner>```* для отображения прогресса загрузки данных, когда длина массива *products* равна нулю, т.е. до того, как данные еще не получены с сервера REST API.

Затем мы перебрали массив products с помощью **ngFor** и использовали Material card для отображения названия, цены, количества, описания и изображения (соответственно *name*, *price*, *quantity*, *description* и *image*) каждого товара.

Это скриншот главной страницы после получения данных JSON:

![](https://i.postimg.cc/y6Sd6tDr/46.jpg)

### Этап 9. Добавление обработки ошибок HTTP с помощью RxJS catchError() и HttpClient

Методы HttpClient можно с легкостью использовать оператором *catchError()* из RxJS, т.к. они возвращают Observable, через метод *pipe()* для отлова и обработки ошибок. Нам просто нужно определить метод обработки ошибок в нашей службе.

Есть 2 типа ошибок в приложениях фронт-энда:

- Ошибки на стороне клиента, такие как сетевые проблемы и ошибки синтаксиса и типов JavaScript. Эти ошибки возвращают объекты *ErrorEvent*.

- Ошибки на стороне сервера, такие как ошибки кода на сервере и ошибки доступа к базе данных. Эти ошибки возвращают HTTP Error Responses.

Таким образом, нам просто нужно проверить, является ли ошибка экземпляром ErrorEvent, чтобы получить тип ошибки для того, чтобы мы могли обработать ее соответствующим образом.

Давайте рассмотрим это на примере. Открываем файл *data.service.ts* и обновляем его соответствующим образом:
```js
import { Injectable } from '@angular/core';
import { HttpClient, HttpErrorResponse } from "@angular/common/http";

import {  throwError } from 'rxjs';
import { retry, catchError } from 'rxjs/operators';

@Injectable({
  providedIn: 'root'
})
export class DataService {

  private REST_API_SERVER = "http://localhost:3000/products";

  constructor(private httpClient: HttpClient) { }

  handleError(error: HttpErrorResponse) {
    let errorMessage = 'Unknown error!';
    if (error.error instanceof ErrorEvent) {
      // Client-side errors
      errorMessage = `Error: ${error.error.message}`;
    } else {
      // Server-side errors
      errorMessage = `Error Code: ${error.status}\nMessage: ${error.message}`;
    }
    window.alert(errorMessage);
    return throwError(errorMessage);
  }

  public sendGetRequest(){
    return this.httpClient.get(this.REST_API_SERVER).pipe(catchError(this.handleError));
  }
}
```

Как мы видим, это должно быть для каждой службы в нашем приложении, что и хорошо для нашего примера, т.к. он содержит только одну службу, но как только проект начнет расти со многими службами, которые могут выдавать все ошибки, нам нужно использовать лучшие решения вместо использования метода *handleError* для каждой службы, которая подвержена ошибкам. Одно из такие решений состоит в том, чтобы обрабатывать ошибки глобально в нашем Angular-проекте с помощью [перехватчиков HttpClient](https://angular.io/guide/http#http-interceptors).

Это скриншот ошибки в консоли, если сервер недоступен:

![](https://i.postimg.cc/HWK6Xcsk/47.jpg)

### Этап 10. Повторная отправка HTTP-запросов в случае неудачи с помощью RxJS Retry()

На данном этапе нашего урока Angular мы увидим, как используется оператор *retry()* RxJS с HttpClient для автоматической повторной подписки на возвращаемый Observable, что приводит к повторной отправке неудачных HTTP-запросов.

Во многих случаях ошибки являются временными и из-за плохих условий работы сети, поэтому повторная попытка автоматически устраняет их. Например, в мобильных устройствах часты перебои в работе сети, поэтому, если пользователь попытается снова, он может получить успешный ответ. Вместо того, чтобы позволить пользователям повторить попытку вручную, давайте посмотрим, как это сделать автоматически в нашем примере приложения.

Библиотека RxJS предоставляет несколько операторов повтора. Среди них есть оператор *retry()*, который позволяет автоматически переподписать на RxJS Observable заданное количество раз. Переподписка на Observable, возвращаемый методом HttpClient, приводит к повторной отправке HTTP-запроса на сервер, поэтому пользователям не нужно повторять операцию или перезагружать приложение.

Мы можем использовать оператор RxJS *retry()*, передавая его (используя метод *pipe()*) в Observable, возвращаемый из метода HttpClient перед обработчиком ошибок.

Открываем файл *data.service.ts* и импортируем оператор *retry()*:

```js
import { retry, catchError } from 'rxjs/operators';
```

Обновляем метод *sendGetRequest()*:

```js
public sendGetRequest(){
    return this.httpClient.get(this.REST_API_SERVER).pipe(retry(3),catchError(this.handleError));
  }
```

Это приведет к повторной попытке отправки неудачного HTTP-запроса три раза.

### Этап 11. Отмена подписки от HttpClient Observables с помощью RxJS takeUntil()

Здесь мы узнаем, почему нам нужно и как отписаться от Obsrevables в нашем коде с помощью оператора *takeUntil()*.

Прежде всего, нам ли нам отписаться от Observables, возвращаемых методами HttpClient? Как правило, нам нужно вручную отписаться от любых подписанных RxJS Observables в наших компонентах Angular, чтобы избежать утечек памяти, но в случае с HttpClient это автоматически обрабатывается Angular путем отписки при получении HTTP-ответа. Однако в некоторых случаях необходимо отписаться вручную, например, отменить ожидающие запросы, когда пользователь собирается покинуть компонент.

Мы можем просто вызвать метод *unsubscride()* из объекта *Subscription*, возвращаемого методом *subscribe()* в методе жизненного цикла **ngOnDestroy()** компонента, чтобы отписаться от Observable.

Также существует лучший способ отменить подписку или завершить Observables – использовать оператор *takeUntil()*.

[Оператор *takeUntil()*](https://rxjs.dev/api/operators/takeUntil) выдает значения, испускаемые источником Observable до тех пор, пока уведомитель Observable не выдаст значение.

Давайте посмотрим, как использовать этот оператор для завершения Observables, когда компонент уничтожается.

Откроем файл *home.component.ts* и обновим код:

```js
import { Component, OnInit, OnDestroy } from '@angular/core';
import { DataService } from '../data.service';
import { takeUntil } from 'rxjs/operators';
import { Subject } from 'rxjs';

@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
export class HomeComponent implements OnInit, OnDestroy {

  products = [];
  destroy$: Subject<boolean> = new Subject<boolean>();

  constructor(private dataService: DataService) { }

  ngOnInit(){
    this.dataService.sendGetRequest().pipe(takeUntil(this.destroy$)).subscribe((data: any[])=>{
      console.log(data);
      this.products = data;
    })
  }
  ngOnDestroy(){
    this.destroy$.next(true);
    // Отписываемся от Subject
    this.destroy$.unsubscribe();
  }

}
```

Сначала мы импортировали интерфейс *OnDestroy*, *Subject* и оператор *takeUntil()*. Затем мы реализовали интерфейс *OnDestroy* и добавили хук жизненного цикла *ngOnDestroy()* к компоненту.

Далее мы создали экземпляр Subject, который может выдавать логические значения (тип значения в данном примере действительно не имеет значения), которого будем использовать в качестве уведомителя оператора *takeUntil()*.

Затем, в хуке жизненного цикла *ngOnInit()*, мы вызвали *sendGetRequest()* нашей службы данных и вызвали метод *pipe()* возвращаемого Observable для передачи оператору *takeUntil()* и, наконец, мы подписались на комбинированный Observable. В теле метода subscribe() мы добавили логику, чтобы поместить полученные данные HTTP-ответа в массив **products**.

Оператор *takeUntil()* позволяет уведомляемому Observable выдавать значения до тех пор, пока значение не будет выдано от уведомителя Observable.

Когда Angular уничтожает компонент, он вызывает метод жизненного цикла **ngOnDestroy()**, который в нашем случае вызывает метод *next()* для выдачи значения, так что RxJS завершает все подписанные Observables.

Вот и все. На данном этапе мы добавили логику отмены любого ожидающего HTTP-запроса путем отказа от подписки на возвращаемый Observable в случае, если пользователь решит перейти от одного компонента к другому до получения HTTP-ответа.

### Этап 12. Добавление параметров URL-запроса в метод HttpClient *get()*

Здесь мы начнем добавлять логику для реализации пагинации в наше приложение. Мы узнаем, как используются параметры URL-запроса через ***fromString*** и ***HttpParams*** для предоставления соответствующих значений параметров _page и _limit оконечной точки /products нашего сервера JSON REST API для получения разбитых на страницы данных.

Открываем файл *data.service.ts* и добавляем импорт HttpParams:

```js
import { HttpClient, HttpErrorResponse, HttpParams } from "@angular/common/http";
```
Затем обновим метод *sendGetRequest()* следующим образом:

```js
public sendGetRequest(){
  // Add safe, URL encoded_page parameter
  const options = { params: new HttpParams({fromString: "_page=1&_limit=20"}) };
  return this.httpClient.get(this.REST_API_SERVER).pipe(retry(3),catchError(this.handleError));
}
```

Мы использовали **HttpParams** и **fromString** для создания параметров HTTP-запроса из строки *_page=1&_limit=20*. Это говорит о том, что возвращает первую страницу из 20 товаров.

Теперь ***sendGetRequest()*** будет использоваться для получения первой страницы данных. Полученный HTTP-ответ будет содержать заголовок Link с информацией о первой, предыдущей, следующей и последней ссылках страницы данных.

### Этап 13. Получение полного HTTP-ответа с помощью Angular HttpClient

На этом этапе мы продолжим реализацию логики извлечения информации о разбиении на страницы из заголовка Link, содержащегося в HTTP-ответе, полученном от сервера JSON REST API.

По умолчанию, HttpClient предоставляет только тело ответа, но в нашем случае нам нужно разобрать (или анализировать, т.е. спарсить) заголовок Link для ссылок разбиения на страницы, потому мы должны сообщить HttpClient, что мы хотим получить полный **HttpResponse**, используя опцию *observe*.

Переходим в файл *data.service.ts* и импортируем оператор RxJS *tap()*:

```js
import { retry, catchError, tap } from 'rxjs/operators';
```

Затем определяем следующие строковые переменные:

```js
public first: string = "";
public prev: string = "";
public next: string = "";
public last: string = "";
```

Далее определяем метод *parseLinkHeader()*, который парсит заголовок Link и заполняет переменные соответствующим образом:

```js
parseLinkHeader(header) {
  if (header.length == 0) {
    return ;
  }

  let parts = header.split(',');
  var links = {};
  parts.forEach( p => {
    let section = p.split(';');
    var url = section[0].replace(/<(.*)>/, '$1').trim();
    var name = section[1].replace(/rel="(.*)"/, '$1').trim();
    links[name] = url;

  });

  this.first  = links["first"];
  this.last   = links["last"];
  this.prev   = links["prev"];
  this.next   = links["next"]; 
}
```
  
Потом обновим *sendGetRequest* как показано ниже:

```js
public sendGetRequest(){
  // Add safe, URL encoded _page and _limit parameters 
  return this.httpClient.get(this.REST_API_SERVER, {  params: new HttpParams({fromString: "_page=1&_limit=20"}), observe: "response"}).pipe(retry(3), catchError(this.handleError), tap(res => {
    console.log(res.headers.get('Link'));
    this.parseLinkHeader(res.headers.get('Link'));
  }));
}
```

Мы добавили опцию observe со значением *response* в параметре опций метода *get()*, чтобы получить полный HTTP-ответ с заголовками. Далее мы используем оператор RxJS *tap()* для парсинга заголовка Link перед возвратом завершенного Observable.

Поскольку функция *sendGetRequest()* теперь возвращает Observable с полным HTTP-ответом, нам нужно обновить компонент home, поэтому открываем файл *home.component.ts* и импортируем *HttpResponse*:

```js
import { HttpResponse } from '@angular/common/http';
```

Далее обновляем метод *subscribe()*:

```js
ngOnInit() {
  this.dataService.sendGetRequest().pipe(takeUntil(this.destroy$)).subscribe((res: HttpResponse<any>)=>{
    console.log(res);
    this.products = res.body;
  })  
}
```

Теперь можем получить доступ к данным из объекта *body* полученного HTTP-ответа.

Возвращаемся к файлу *data.service.ts* и добавляем новый метод:

```js
public sendGetRequestToUrl(url: string){
  return this.httpClient.get(url, { observe: "response"}).pipe(retry(3), catchError(this.handleError), tap(res => {
    console.log(res.headers.get('Link'));
    this.parseLinkHeader(res.headers.get('Link'));

  }));
}
```

Этот метод аналогичен sendGetRequest() за исключением того, что он принимает URL-адрес, на который нам нужно отправить HTTP-запрос GET.
Возвращаемся к файлу home.component.ts и добавляем определение следующих методов:

```js
public firstPage() {
  this.products = [];
  this.dataService.sendGetRequestToUrl(this.dataService.first).pipe(takeUntil(this.destroy$)).subscribe((res: HttpResponse<any>) => {
    console.log(res);
    this.products = res.body;
  })
}
public previousPage() {

  if (this.dataService.prev !== undefined && this.dataService.prev !== '') {
    this.products = [];
    this.dataService.sendGetRequestToUrl(this.dataService.prev).pipe(takeUntil(this.destroy$)).subscribe((res: HttpResponse<any>) => {
      console.log(res);
      this.products = res.body;
    })
  }

}
public nextPage() {
  if (this.dataService.next !== undefined && this.dataService.next !== '') {
    this.products = [];
    this.dataService.sendGetRequestToUrl(this.dataService.next).pipe(takeUntil(this.destroy$)).subscribe((res: HttpResponse<any>) => {
      console.log(res);
      this.products = res.body;
    })
  }
}
public lastPage() {
  this.products = [];
  this.dataService.sendGetRequestToUrl(this.dataService.last).pipe(takeUntil(this.destroy$)).subscribe((res: HttpResponse<any>) => {
    console.log(res);
    this.products = res.body;
  })
}
```

Наконец, откроем файл *home.component.html* и обновляем шаблон следующим образом:

```html
<div style="padding: 13px;">
  <mat-spinner *ngIf="products.length === 0"></mat-spinner>

  <mat-card *ngFor="let product of products" style="margin-top:10px;">
      <mat-card-header>
          <mat-card-title>#{{product.id}} {{product.name}}</mat-card-title>
          <mat-card-subtitle>{{product.price}} $/ {{product.quantity}}
          </mat-card-subtitle>
      </mat-card-header>
      <mat-card-content>
          <p>
              {{product.description}}
          </p>
          <img style="height:100%; width: 100%;" src="{{ product.imageUrl }}" />
      </mat-card-content>
      <mat-card-actions>
    <button mat-button> Buy product</button>
  </mat-card-actions>
  </mat-card>

</div>
<div>
  <button (click) ="firstPage()" mat-button> First</button>
  <button (click) ="previousPage()" mat-button> Previous</button>
  <button (click) ="nextPage()" mat-button> Next</button>
  <button (click) ="lastPage()" mat-button> Last</button>
</div>
```

Смотрим, что у нас получилось:

![](https://i.postimg.cc/fyKB8dF3/48.jpg)

### Этап 14. Запрос типизированного HTTP-ответа с помощью Angular HttpClient

На этом этапе мы рассмотрим, как использовать типизированные HTTP-ответы в нашем приложении.

Angular HttpClient позволяет указать тип объекта ответа в объекте запроса, что упрощает использование ответа. А также позволяет подтверждать тип во время компиляции.

Давайте начнем с определения пользовательского типа с помощью интерфейса TypeScript с необходимыми свойствами.

Заходим в терминал и выполняем команду в корневом каталоге нашего проекта:

```sh
  ng generate interface product
```

Открываем файл product.ts и обновляем содержимое файла:

```js
export interface Product {
    id: number;
    name: string;
    description: string;
    price: number;
    quantity: number;
    imageURL: string;
}
```

Далее указываем интерфейс *Product* в качестве типизированного параметра вызова *HttpClient.get()* в службе данных. Идем в файл *data.service.ts* и импортируем интерфейс *Product*:

```js
import { Product } from './product';
```

Потом чуточку переписываем следующий код:

```js
public sendGetRequest(){

  return this.httpClient.get<Product[]>(this.REST_API_SERVER, {  params: new HttpParams({fromString: "_page=1&_limit=20"}), observe: "response"}).pipe(retry(3), catchError(this.handleError), tap(res => {
    console.log(res.headers.get('Link'));
    this.parseLinkHeader(res.headers.get('Link'));

  }));
}

public sendGetRequestToUrl(url: string){
  return this.httpClient.get<Product[]>(url, { observe: "response"}).pipe(retry(3), catchError(this.handleError), tap(res => {
    console.log(res.headers.get('Link'));
    this.parseLinkHeader(res.headers.get('Link'));

  }));
}
```

Открываем файл *home.component.ts* и импортируем интерфейс *Product*:

```js
import { Product } from '../product';
```

Изменяем тип массива *products*, как показано ниже:

```js
export class HomeComponent implements OnInit, OnDestroy {

  products: Product[] = [];
```

Далее изменяем тип HTTP-ответа в вызове sendGetRequest():

```js
ngOnInit() {
  this.dataService.sendGetRequest().pipe(takeUntil(this.destroy$)).subscribe((res: HttpResponse<Product[]>)=>{
    console.log(res);
    this.products = res.body;
  })  
}
```

То же самое нам нужно сделать и для других методов *firstPage()*, *previousPage()*, *nextPage()* и *lastPage()*.

### Этап 15. Сборка и развертывание нашего приложения Angular на хостинге Firebase

На этом этапе мы узнаем, как собрать и развернуть наше приложение на хостинге Firebase с помощью команды **ng deploy**. А также узнаем, как развернуть приложение frontend без поддельного сервера JSON.

В Angular CLI 8.3+ введена новая команда **ng deploy**, которая упрощает развертывание нашего приложения Angular с помощью компоновщика CLI, связанного с нашим проекта. Существует множество сторонних сборщиков, которые реализуют возможности развертывания для разных платформ. Мы можем добавить любой из них в свой проект, выполнив команду **ng add**.

После добавления пакета развертывания он автоматически обновит конфигурацию нашего рабочего пространства (т.е. файл *angular.json*) с разделом развертывания для выбранного проекта. Далее можем использовать команду **ng deploy** для развертывания этого проекта.

Давайте теперь посмотрим на примере развертывание нашего проекта на хостинге Firebase.

Возвращаемся к терминалу, и запускаем команду, находясь в корневом каталоге Angular-проекта:

```sh
 ng add @angular/fire
```

Данная команда добавит возможность развертывания на Firebase в наш проект. А также обновит файл angular.json нашего проекта, добавив этот раздел:

```json
"deploy": {
          "builder": "@angular/fire:deploy",
          "options": {}
        }
```

CLI предложит вставить код авторизации (**Paste authorization code here**), откроет веб-браузер по умолчанию и попросит нас предоставить разрешения Firebase CLI для администрирования нашей учетной записи Firebase:

![](https://i.postimg.cc/TPMgWw7B/49.jpg)

После входа в учетную запись Google, связанную с учетной записью Firebase, нам будет предоставлен код авторизации:

![50.jpg](https://i.postimg.cc/9FkGC1Gm/50.jpg)

Далее нам будет предложено выбрать проект (Please select a project: (Use arrow keys or type to search)). Мы должны были создать проект Firebase ранее.

CLI создаст файлы *firebase.json* и *.firebaserc*, и обновит файл angular.json соответственно.

Потом мы развернем приложение на Firebase, используя команду:
```sh
 ng deploy
```

Эта команда произведет оптимизированную сборку нашего приложения (‘эквивалентно команде **ng deploy --prod**), и загрузит производственные ресурсы на хостинг Firebase.

### Заключение

На протяжении всего этого урока мы создали полностью рабочий проект Angular с использованием последней версии.

[Оригинал](https://www.techiediaries.com/angular/angular-9-8-tutorial-by-example-rest-crud-apis-http-get-requests-with-httpclient/)