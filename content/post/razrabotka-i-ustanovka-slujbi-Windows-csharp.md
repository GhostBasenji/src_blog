+++
title = "Разрабатываем и устанавливаем службу Windows в C#"
date = "2021-06-13"
tags = ["C#", "Windows Service", "Установка и удаление службы Windows"]
+++

В данной статье описывается пошаговый процесс разработки и установки службы Windows для выполнения запланированной работы в зависимости от временного интервала.

<!--more-->

### Пишем код

Запускаем Visual Studio. В появившемся окне щелкаем по **Create a new project**.

![](https://i.postimg.cc/Jz0HFJLd/73.png)

В появившемся окне выбираем **Windows Service (.NET Framework)**.

![](https://i.postimg.cc/Fzh7Vkpp/74.png)

Потом называем проект **TestWindowsService**, как показано ниже.

![](https://i.postimg.cc/768CbWTp/75.png)

После того, как нажали на кнопку **Create**, проект будет создан и мы увидим следующее:

![](https://i.postimg.cc/FFxfsGFB/76.png)

Шелкаем правой кнопкой мыши на файл **Service1.cs** в обозревателе решений и переименовываем его в *Sheduler* или любое другое имя, которое мы захотим ему присвоить. Потом шелкаем по ссылке **“switch to code view”**.

В редакторе кода мы видим 2 метода – **OnStart()** и **OnStop()**. Функция **OnStart()** инициируется во время запуска службы Windows, а функция **OnStop()** – при остановке службы.

```cs
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Diagnostics;
using System.Linq;
using System.ServiceProcess;
using System.Text;
using System.Threading.Tasks;

namespace TestWindowsService
{
    public partial class Sheduler : ServiceBase
    {
        public Sheduler()
        {
            InitializeComponent();
        }

        protected override void OnStart(string[] args)
        {
        }

        protected override void OnStop()
        {
        }
    }
}
```
Щелкаем правой кнопкой по проекту **TestWindowsService**, добавляем новый класс и называем его **Library.cs**. Этот класс будет полезен для создания методов, которые нам нужны в проекте. Если проект TestWindowsService является крупным проектом, то можно создать проект ClassLibrary и обращаться к нему в своем проекте TestWindowsService.

![](https://i.postimg.cc/RF7WtL7q/77.png)

![](https://i.postimg.cc/JhBDrLtN/78.png)

### ***Library.cs***

Делаем класс общедоступным и объявляем его как статический класс.
```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IO;

namespace TestWindowsService
{
    public static class Library
    {
    }
}
```
Создаем метод логгирования (WriteErrorLog) для регистрации исключений.
```cs
public static void WriteErrorLog(Exception ex)
{
    StreamWriter sw = null;
    try
    {
        sw = new StreamWriter(AppDomain.CurrentDomain.BaseDirectory + "\\LogFile.txt", true);
        sw.WriteLine(DateTime.Now.ToString() + ": " + ex.Source.ToString().Trim() + "; " + ex.Message.ToString().Trim());
        sw.Flush();
        sw.Close();
    }
    catch
    {

    }
}
```
Создаем еще один метод (WriteErrorLog) для логгирования пользовательских сообщений.
```cs
public static void WriteErrorLog(string Message)
{
    StreamWriter sw = null;
    try
    {
        sw = new StreamWriter(AppDomain.CurrentDomain.BaseDirectory + "\\LogFile.txt", true);
        sw.WriteLine(DateTime.Now.ToString() + ": " + Message);
        sw.Flush();
        sw.Close();
    }
    catch
    {

    }
}
```

### ***Scheduler.cs***

Теперь возвращаемся в файл *Scheduler.cs* и объявляем *Timer*.
```cs
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Diagnostics;
using System.Linq;
using System.ServiceProcess;
using System.Text;
using System.Threading.Tasks;
using System.Timers;

namespace TestWindowsService
{
    public partial class Sheduler : ServiceBase
    {
        private Timer timer1 = null;

        public Sheduler()
        {
            InitializeComponent();
        }

        protected override void OnStart(string[] args)
        {
        }

        protected override void OnStop()
        {
        }
    }
}
```
Напишем следующий код в методах OnStart() и timer1_Tick():
```cs
protected override void OnStart(string[] args)
{
    timer1 = new Timer();
    this.timer1.Interval = 30000; // Каждые 30 секунд
    this.timer1.Elapsed += new System.Timers.ElapsedEventHandler(this.timer1_Tick);
    timer1.Enabled = true;
    Library.WriteErrorLog("Test window service started");
}

private void timer1_Tick(object sender, ElapsedEventArgs e)
{
    // Здесь пишем код, чтобы выполнить какую-то работу, в зависимости от нужд
    Library.WriteErrorLog("Timer ticked and some job has been done successfully");
}
```
А теперь напишем следующий код в методе OnStop():
```cs
protected override void OnStop()
{
    timer1.Enabled = false;
    Library.WriteErrorLog("Test window service stopped");
}
```

### ***Scheduler.cs [Deisgn]***
Теперь возвращаемся к файлу Scheduler.cs [Design], щелкаем правой кнопкой мыши на окне редактора и выбираем из меню “Add Installer”.

![](https://i.postimg.cc/bNNZGbsN/79.png)

После чего мы увидим, что появится новый файл с именем “ProjectInstaller.cs”.

![](https://i.postimg.cc/MKdjt5hQ/80.png)

![](https://i.postimg.cc/cLztGH11/81.png)

Щелкаем правой кнопкой мыши на “serviceInstaller1” и выбираем “Properties”.

![](https://i.postimg.cc/2yT3cjXD/82.png)

Изменяем имя “ServiceName” на “Test Windows Service”, выбираем в свойстве StartType “Manual” (можно выбрать “Automatic”, если нужно, чтобы служба запускалась автоматически).

![](https://i.postimg.cc/yYQk0dZh/83.png)

Щелкаем правой кнопкой мыши на serviceProccessInstaller1, переходим в окно свойств и ставим в свойстве Account “LocalSystem”.

![](https://i.postimg.cc/0yzrnsYT/84.png)

Собираем проект. Теперь должен у нас появится файл .exe там, где мы создали проект.

![](https://i.postimg.cc/MTSTzfCw/85.png)

Вот и все. Наша служба Windows полностью готова к установке на нашей машине.

### Устанавливаем службу Windows
Запускаем **Developer Command Prompt for VS2019** (**Start** > **Microsoft Visual Studio 2019**).

Введем следующую команду:
```sh
cd  <физ.местоположение нашего файла TestWindowsService.exe>
```
В нашем случае это:
```sh
cd D:\repos\TestWindowsService\TestWindowsService\bin\Debug
```

![](https://i.postimg.cc/9fT03YN1/86.png)

Далее напишем команду:
```sh
InstallUtil.exe “TestWindowsService.exe”
```
и нажимаем клавишу Enter.

![](https://i.postimg.cc/zG4vPcpV/87.png)

Вот и все, TestWindowsService успешно установлен.

![](https://i.postimg.cc/Jn5h048k/88.png)

### Запускаем службу Windows

Так как мы выбрали StartType = Manual, значит, мы должны запустить службу Windows вручную, зайдя в приложение “Services”.

![](https://i.postimg.cc/PrxqfjRC/89.png)

Находим и щелкаем по службе “TestWindowsService” и щелкаем по Start, чтобы запустить службу. После чего идем в папку с файлом TestWindowsService.exe, чтобы просмотреть логи.

### LogFile.txt

Поскольку мы отслеживаем нашу службу Windows, записывая некоторые логи в файл .txt под названием LogFile.txt, мы можем протестировать рабочее состояние нашей службы, просмотрев этот файл логов.

После запуска службы Windows появится файл LogFile.txt, который находится по адресу нашего проекта

![](https://i.postimg.cc/NFGjHqGP/90.png)

Щелкаем по LogFile.txt, чтобы просмотреть логи, выполняется ли наша служба ту работу, на которую мы настроили, каждые 30 секунд.

![](https://i.postimg.cc/rshFGnKy/91.png)

Как видим, наша служба исправно работает так, как мы хотим, с интервалом в 30 секунд.

### Останавливаем службу Windows
Чтобы остановить службу Windows, просто щелкаем по ссылке “Stop” в окне Services, выделив нашу службу TestWindowsService.
Журнал логов после остановки нашей службы:

![](https://i.postimg.cc/59p0M0nc/92.png)

### Удаляем службу Windows

Запускаем **Developer Command Prompt for VS2019** (**Start** > **Microsoft Visual Studio 2019**).

Введем следующую команду:
```sh
cd  <физ.местоположение нашего файла TestWindowsService.exe>
```

В нашем случае это:
```sh
cd D:\repos\TestWindowsService\TestWindowsService\bin\Debug
```

Далее напишем команду:
```sh
InstallUtil.exe /u “TestWindowsService.exe”
```
и нажимаем клавишу Enter.

После выполнения предыдущих команд служба TestWindowsService будет успешно удалена с нашего компьютера.

Вот и все.