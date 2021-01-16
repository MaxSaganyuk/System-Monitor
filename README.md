# System-Monitor
Utility that allows to monitor system and hardware information, such as temperatuge, CPU usage and so on

#### На данный момент проэкт находится на стадии разработки

### Краткое описание проекта
Проект являет собой ПО позволяющее отслеживать состояние ресурсов компьютера. ПО состоит из трех частей - две программные и одна аппаратная.
1) Первая часть: основная программа(описаная в этом репозитории).
2) Вторая часть: прошивка для Arduino(//ссылка на репозиторий).
3) Третья часть: дисплей IIC I2C для arduino, 4-контактный, 0.96 дюйм, дисплей 1602 с интерфейсной шиной IIC/I2C, Arduino Uno/Arduino Nano

### Основная программа System Monitor
Основная программа состоит из 4-х владок:
1) Overview
2) Monitoring tools
3) Monitoring tool global
4) External display tools

Рассмотрим их подробней

#### Вкладка Overview

Вкладка Overview содержит в себе информацию о времени с момента запуска системы (Up Time) на Рис. 1.1, информацию про апаратные составляющие компьютера на котором была запущенна программа, а именно название, модель и температуру материнской платы, ЦП, видеокарты, ОЗУ, хранилища, аудио адаптера, привода оптических дисков, сетевого контролера. При достижении температуры любого из устройств до критической отметки программа будет отправлять пользователю сообщение об этом.

<p align = "center">
<img src = "readMeImages/overview1.png"><br>
  Рис. 1.1 Список названия оборудования и его температура
</p>
Ниже расположен график, который выводит информацию  о температуре выбраного устройства в реальном времени. (рис. 1.1). График отображается для выбраного пользователем устройства (выбор производится нажатием на необходимое устройство из списка на рис. 1.1)

<p align = "center">
<img src = "readMeImages/overview2.png"><br>
  Рис. 1.2 График изменения температуры для выбраного устройства
</p>
В правой части вкладки расположена информация о текущих драйверах для устройств, в виде: устройство - драйвер.

<p align = "center">
<img src = "readMeImages/overview3.png">
  Рис. 1.3 Информаиця о драйверах устройств
</p>
Ниже расположен список имен текущих процессов.

<p align = "center">
<img src = "readMeImages/overview4.png"><br>
  Рис. 1.4 Список текущих процессов
</p>
Еще ниже отображается загрузка ЦП и ОЗУ на данный момент.

<p align = "center">
<img src = "readMeImages/overview5.png"><br>
  Рис. 1.5 Текущая нагрузка ЦП и ОЗУ
</p>

#### Вкладка Monitoring tools

Данная вкладка позволяет отслеживать нагрузку на ЦП и ОЗУ создаваемую процессами. Пользователь задает допустимую нагрузку для ЦП (в процентах) или/и для ОЗУ (в килобайтах), так же для нагрузки на ОЗУ можно выбрать отслеживание по приватному набору или по рабочему набору. Есть два типа выдачи информации про превышение нагрузки: <i>сообщение</i>, при котором при превышении допустимой нагрузки пользователю выдается сообщение в виде дата, время, процесс который вызвал нагрузку, нагрузка, после выдачи сообщения процесс мониторинга останавливается и при необходимости его нужно запускать снова, это сделано для того что-бы не заспамить пользователя однообразными сообщениями; лог - при выборе этого типа вывода информации создается файл(имя может задать пользователь иначе будет использоваться стандартное имя - дата время создания файла и идентификатор того, что программа будет мониторить - ЦП или ОЗУ, то есть стандартное имя файла будет например таким: "Thu Jan 14 18.27.16 2021_RAM"), при превышении допустимого значения нагрузки в файл будет записано информация в таком же виде как и при выборе вывода сообщением, процесс логирования не будет остановлен пока пользователь не прекратит его. 

Пользователь может добавить процессы которые будут игнорироваться, то есть, если процесс А превышает нагрузку, но он добавлен в список игнорирования, то пользователь не получит сообщения о превышении нагрузки процессом А.

Рассмотрим интерфейс

В верхней части окна расположены инструменты мониторинга ЦП:

<p align = "center">
<img src = "readMeImages/monitoringtools1.png"><br>
  Рис. 2.1 Интерфейс вкладки Monitoring tools, инструменты мониторинга ЦП
</p>

Рассмотрим инструменты мониторинга ЦП. Для начала работы необходимо поставить галочку около Monitor processes(CPU Load) (Рис. 2.1), после чего станет активным поле ввода допустимой нагрузки, выбор файлов для игнорирования и подсказка.

<p align = "center">
<img src = "readMeImages/monitoringtools2.png"><br>
  Рис. 2.2 Инструменты мониторинга ЦП в активном состоянии
</p>

Введем допустимую нагрузку в 40 процентов и запустим программа нажав кнопку <i>Apply<i/>
  
<p align = "center">
<img src = "readMeImages/monitoringtools3.png"><br>
  Рис. 2.3 Запуск мониторинга ЦП
</p>

Теперь создадим нагрузку на ЦП сторонней программой и посмотрим на результат работы программы.

<p align = "center">
<img src = "readMeImages/monitoringtools4.png"><br>
  Рис. 2.4 Результат мониторинга ЦП
</p>

Как видим программа сообщает пользователю о прекращении мониторинга сменив метку "Monitoring..." (Рис. 2.3) на "Stop". Так же видим сообщение с текстом сообщающим время, название процесса и нагрузку создаваемую процессом. Так же видим, что теперь активна кнопка <i>Reset</i>, нажав на нее получим исходный вид окна:

<p align = "center">
<img src = "readMeImages/monitoringtools5.png"><br>
  Рис. 2.5 Окно после нажатия кнопки Reset
</p>

Теперь выберем другой тип вывода информации на лог, так же укажем имя файла как helloGitHub:

<p align = "center">
<img src = "readMeImages/monitoringtools6.png"><br>
  Рис. 2.6 Тип вывода Log
</p>

После нажатия кнопки <i>Apply<i/> проверим папку с программой:
  
<p align = "center">
<img src = "readMeImages/monitoringtools7.png"><br>
  Рис. 2.7 Созданый файл с именем helloGitHub
</p>

Как видим был создан файл с именем helloGitHub_CPU (идентификатор CPU, говорит о том, что это лог мониторинга ЦП). Теперь остановим процесс мониторинга:

<p align = "center">
<img src = "readMeImages/monitoringtools8.png"><br>
  Рис. 2.8 Остановка процесса мониторинга
</p>

Как видим имеем такую же смену метки "Monitoring" на мету "Stop", говорящую об остановке процесса мониторинга. Теперь проверим сам лог:

<p align = "center">
<img src = "readMeImages/monitoringtools9.png"><br>
  Рис. 2.8 Созданый ранее лог
</p>
