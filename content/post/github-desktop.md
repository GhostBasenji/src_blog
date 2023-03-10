+++
title = "Работаем с GitHub Desktop"
date = "2021-06-05"
tags = ["GitHub Desktop"]
+++

В этой статье осваиваем GitHub Desktop на практике, а именно:
- Установка и аутентификация GitHub Desktop
- Создание репозитория Git
- Добавление в репозиторий новый или существующий проект

<!--more-->

### Установка и аутентификация GitHub Desktop

Скачаем и установим GitHub Desktop [GitHub desktop]. Запускам приложение и авторизируемся (по идее у нас уже есть аккаунт на GitHub, но если нет, то создаем его).

Можно безопасно пройти аутентификацию с помощью своей учетной записи и получить доступ к ресурсам из GitHub Desktop.
Открываем GitHub Desktop. Щелкаем по **File** > **Options…**, как показано ниже.

![](https://i.postimg.cc/K8934TKr/51.png)

![](https://i.postimg.cc/MZRBtX4q/52.png)

Вот как мы можем аутентифицироваться и подключаться к GitHub в GitHub Desktop.

### Создание репозитория Git на GitHub
В этом разделе мы научимся создавать новые репозитории Git на GitHub с помощью GitHub Desktop.
Щелкаем по File в GitHub Desktop, как показано ниже.

![](https://i.postimg.cc/pXHFSRb8/53.png)

Мы получаем возможность создать новый репозиторий. Кроме того, есть и другие варианты, такие как добавление локального репозитория, клонирование репозитория.

Итак, мы выбираем **New repository…**. После чего перед нами появится окно со следующими вариантами создания репозитория Git.

![](https://i.postimg.cc/FzjJKnc7/54.png)

Теперь рассмотрим следующие поля и введем соответственно им данные.

* **Name**. Имя git-репозитория. В нашем случае имя – demoGithub.
* **Description**. Тут дается описание репозитория.
* **Local path**. Выбирается локальный путь для репозитория, в котором будет храниться фактический проект локально.
* **Initialize this repository with a README**. Создается файл README. Рекомендуется добавлять этот файл для каждого проекта, т.к. можно быстро получить подробную информацию о проекте, изменениях и версиях.
* **Git ignore**. Добавляет файл ***.gitignore***, в котором указывается список определенных лишних файлов, которых нужно игнорировать или не добавлять в репозиторий. В выпадающем списке выбирается шаблон .gitignore определенного языка того или иного проекта.

![](https://i.postimg.cc/9037CjD6/55.png)

* **License**. В выпадающем списке выбирается лицензия для репозитрия. Тут мы будем по умолчанию выбираем лицензию MIT.

![](https://i.postimg.cc/76J2FLZ1/56.png)

После того, как ввели значения, мы щелкаем по кнопке **Create repository**. Мы увидим, что в GitHub Desktop создался репозиторий.

![](https://i.postimg.cc/FK7dSK3t/57.png)

Мы можем увидеть следующие вещи:
1.	Текущий репозиторий demoGithub
2.	Текущая ветка – main
3.	Публикация своего репозитория на GitHub
4.	Опция коммита

Мы начнем с публикации репозитория, нажав на него, как показано ниже.

![](https://i.postimg.cc/nhVQH2Lh/58.png)

После того, как нажали на Publish repository, перед нами появится окно со следующими опциями.

![](https://i.postimg.cc/YqzWKZMP/59.png)

У нас есть возможность выбрать GitHub.com или Enterprise. Мы выбираем бесплатный GitHub.com. Заполняем следующие поля.

* **Name**. Это название git-репозитория в GitHub.com
* **Description**. Описание репозитория.
* **Keep this code private**. Если установить галочку, то git-репозиторий становится приватным, в противном случае – публичный. В данном случае я снимаю галочку, чтобы сделать репозиторий открытым.

Как только щелкнем по **Publish repository**, репозиторий будет создан на GitHub.

![](https://i.postimg.cc/KYwKDyD1/60.png)

Итак, мы успешно создали git-репозиторий и отправили его на GitHub с помощью GitHub Desktop.

### Добавление новый или существующий проект в репозиторий

Это легко. Мы можем создать новый проект или добавить существующий проект в наш локальный репозиторий, как показано ниже

![](https://i.postimg.cc/661PVjDD/61.png)

Затем откроется папка локального репозитория.

![](https://i.postimg.cc/Y9rPRJ2w/62.png)

В связи с этим мы создадим новый проект в том же месте – этим самым мы можем добавить проект в репозиторий GitHub. Давайте создадим проект ASP.NET Core в Visual Studio, как показано ниже.

![](https://i.postimg.cc/gjrTF86S/63.png)
![](https://i.postimg.cc/fL8rrBkS/64.png)

Итак, мы успешно создали наш учебный проект.

![](https://i.postimg.cc/8zLnS1jS/65.png)

После того, как мы создали проект, заходим в GitHub Desktop. В нем увидим все файлы нашего учебного проекта в списке изменений GitHub Desktop.

![](https://i.postimg.cc/Gprg3Zys/66.png)

Теперь мы можем добавить комментарий к изменениям и нажать на кнопку **Commit**.

![](https://i.postimg.cc/wTCbZtx2/67.png)

Мы коммитируем все как есть. Однако, если захотим, то можем снять галочки с файлов или папок, с которыми мы хотим отменить изменения.

После того, как закоммитили, мы увидим окно, в котором нужно отправить коммиты на удаленный репозиторий в GitHub.

![](https://i.postimg.cc/dtkx5RFD/68.png)

Мы видим, что 1 коммит ожидает отправки на GitHub. До сих пор мы коммитили изменения только в локальный репозиторий. А теперь пора отправлять коммиты в удаленный репозиторий.

Мы щелкаем по кнопке **Push Origin**, чтобы отправить проект на GitHub Online. Сразу после нажатия по кнопке GitHub Desktop начнет перемещать все коммиты на удаленный репозиторий.

![](https://i.postimg.cc/QCPnXCQX/69.png)

Мы добавили проект на GitHub и закоммитили его. Мы можем увидеть этот проект на сайте GitHub.

![](https://i.postimg.cc/R0RsWX7p/70.png)

Итак, мы успешно создали локальный git-репозиторий, добавили проект в этот репозиторий, потом запушили на сайт GitHub с помощью GitHub Desktop.

Аналогично, мы можем добавлять существующие проекты в git-репозиторий на Github, как мы делали для нового проекта. Мы можем скопировать проект в этот репозиторий и проверить изменения в GitHub Desktop.

### Вносим и коммитим изменения в проект

Давай внесем некоторые изменения в файлы проекта и закоммитим их с помощью GitHub Desktop. Итак, мы просто немного изменим страницу index проекта, а в GitHub Desktop мы мгновенно увидим список изменений.

![](https://i.postimg.cc/Y9CXYY8r/71.png)

Далее коммитим эти изменения и пушим в удаленный репозиторий. После чего заходим на сайт GitHub и видим, что изменения зафиксированы:

![](https://i.postimg.cc/C1rcN56j/72.png)