+++
title = "Эпизод 1. Создание приложения Electron"
date = "2021-09-10 11:31:06"
tags = ["Electron", "javascript", "VS Code"]
+++

Первой записью мы начинаем серию эпизодов осваивания Electron. 
Здесь впервые запускаем наше приложение Electron.

<!--more-->

Большинство эпизодов будет довольно короткими.
Весь код находится в [этом репозитории github](https://github.com/GhostBasenji/episodes_electron), разбитый по эпизодам.

#### Начало работы
Итак, предположим, что у нас уже установлен [node.js](https://nodejs.org/en/download/).

Создаем новую папку с именем “episode_01”, перейдем в эту папку и напишем следующие команды в консоли:
```sh
npm init -y
npm install --save-dev electron
npx electron .
```
Перед нами появится сообщение “Cannot find module 'index.js'. Please verify that the package.json has a valid "main" entry”. Это говорит о том, что не найден файл **index.js**. Окей, создаем файл **index.js**.

Теперь нам нужно испортировать кое-что из пакета electron, создать окно и загрузить файл для его отображения. Потом полезно иметь еще один код – для закрытия приложения, когда это главное окно закрывается.
```js
let { app, BrowserWindow } = require("electron")

function createWindow() {
  let win = new BrowserWindow({})
  win.maximize()
  win.loadFile("index.html")
}

app.on("ready", createWindow)

app.on("window-all-closed", () => {
  app.quit()
})
```

Создаем файл **index.html**:
```html
<!DOCTYPE html>
<html>
  <body>
    <h1>Welcome to the Electron!</h1>
  </body>
</html>
```
А теперь запустим приложение с помощью команды:
```sh
npx electron .
```
перед нами появится окно, которое только что мы создали

![](https://i.postimg.cc/kXZrJWkb/93.png)

**Оригинал**: [Electron Adventures. Episode 1: Creating New Electron App](https://dev.to/taw/electron-adventures-episode-1-creating-new-electron-app-5oh)