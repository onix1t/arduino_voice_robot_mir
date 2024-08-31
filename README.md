# Инструкция по сборке робота с AI-модулем голсового управления на Aruduino
## 1 Сборка корпуса робота
### 1.1 Подготовка инструментов и деталей
  Набор корпуса включает в себя следующий список деталей:
  
  - 2 платформы корпуса
  - 4 моторчика
  - 4 колеса
  - 4 диска-енкодера
  - 8 крепежей для моторов
  - 12 обычных винтов
  - 8 длинных винтов
  - 8 гаек
  - 6 стоек

  > [!NOTE]
  > Изображение всего набора деталей для сборки корпуса
  
  Из инструментов нам будет достаточно крестовой отвёртки и гаечного ключа соответствующих размеров.
### 1.2 Установка моторчиков
  Детали для даннного этапа:
  
  - 1 платформа
  - 4 моторчика
  - 8 крпежей для мотора
  - 8 длинных винтов
  - 8 гаек

  В первую очередь нам нужно взять платформу и найти следующие отверстия и вырезы для крепяжей моторов.
    
  > [!NOTE]
  > Изображение платформы с обозначенными вырезами
  
  Далее мы берём один из крепяжей и вставляем широкой частью вниз в указанное на рисунке выше отверстие платформы. Подставляем к вставленному крепежу моторчик и берём второй крепёж, который сопоставляем с указанным выше вырезом.
  Сопостовляем отверстия на крепежах и моторе и затем вставляем в них длинные винты. 
  Закрепляем винты гайками при помощи гаячного ключа.
  
  > [!NOTE]
  > Изображение вставленных и зареплённых винтов

  Установка одного мотора закончена, теперь нужно закрепить остальные три моторчика аналогичным способом. 
  
### 1.3 Сборка колёс
  Сборку колёс мы начнём установки дисков-енкодеров. Они устанавлваются с внутренней стороны вращательного элемента мотора.
  
  > [!NOTE]
  > Изображение установленных дисков-энкодеров

  Теперь, мы установим само колёса. Сопосотавим отверстия на самих колёсах и на моторах.

  > [!NOTE]
  > Изображение установленных колёс

### 1.4 Установка верхней части
  Последним этапом сборки является установка верхней платформы. Для её установки нам понадобится:

  - 6 стоек
  - 12 обычных винтов
  - 1 платформа корпуса

  Стойки нужно закрепить винтами при помощи крестовой отвёртки в следующие отверстия на платформе с моторами:

  > [!NOTE]
  > Изображение установленных колёс

  Теперь остаётся взять верхнюю платфому, сопоставить её с отверстиями для стоек и закрепить винтами.

  > [!NOTE]
  > Изображение установленной верхней 
  
## 2 Программа управления роботом
### 2.1 Подкотовка к написанию кода
  Для того чтобы начать написание кода для Arduino нам нужно установить драйвер для платы, а так же специальную среду разработки Arduino IDE с оффициального сайта производителя.
  
  [Ссылка на драйвер Arduino UNO](https://iarduino.ru/file/126.html)
  
  [Ссылка на Arduino IDE](https://www.arduino.cc/en/software)
  
### 2.2 Написаниие кода
  Теперь когда мы установили всё нужное програмное обеспечение для написания кода, мы открываем Arduino IDE и нажимаем на кнопку создания нового скетча.
  Перед началом, нам стоит определиться каким способом Arduino будет принимать информацию с голосового модуля.
  Есть три способа:
  
  - UART
  - I2C
  - SPI

  Для наших задач нам больше всего подойдёт UART или I2C, так как они просты в подключении и требуют меньше проводов, чем SPI. В данной инструкции мы будем рассматривать подключение через I2C, так как передача данных него быстрее, чем на UART, а так же данный тип подключения поддерживает связь с несколькими устройствами на одной шине. Это позволяет легко подключить несколько датчиков, модулей или контроллеров на одной линии (SDA и SCL), что экономит количество проводов и упрощает схему.

### 2.3 Итоговый код
  В результате мы получили скетч, который обрабатывает запросы с голосового модуля через I2C и подаёт сигналы действий на моторчики.
## 2.4 Перенос кода на Arduino

## 3 Сборка логической части робота
### 3.1 Подгтовка инструментов и деталей
  Логическая часть робота состоит из:

  - Плата Arduino
  - Драйвер L298N
  - AI-модуль голсового управления
  - Источник питания 9V
  - Провода

Из инструментов нам будет достаточно крестовой отвёртки соответствующего размера.

### 3.2 Подключение моторчиков
  Драйвер L298N является связной частью для питания всех логических частей робота и самих моторчиков. Начнём с подключения моторчиков. Для них на драйвере есть четыре клемы: OUT1, OUT2, OUT3 и OUT4.
  Подключаем сгруппированные провда так, как это показано на схеме ниже.

  ![Motors](https://github.com/user-attachments/assets/6e702409-39c7-4e78-8de5-9bc0e80573f2)

  > [!IMPORTANT]
  > Во время сборки корпуса провода питания моторчиков были сгруппированы парами: плюс с плюсом и минус с минусом.
  > Сами моторчики установлены так, чтобы програмно можно было подавать сигнал отдельно на правые колёса машины и отдельно на левые колёса. Сделано это для того, чтобы реаллизовать поворот вправо и влево.

### 3.3 Подключение источника питания к L298N
  Теперь мы подключим источник питания к драйверу. Для этого на плате есть клемы 12V и GND. Подключаем плюс к 12V и минус к GND. Оставшуюся клему 5V мы оставим для подключения питания Arduino и голосового модуля.

  ![Power](https://github.com/user-attachments/assets/83059d02-cd3a-4de2-a9ce-6eb517b76672)

  > [!WARNING]
  > При подключении к драйверу источник питания должен быть выключен!

### 3.4 Подключение голсового модуля к Arduino
  Перед тем подключить логическую часть к питанию мы должны подключить голосовой модуль к Arduino, чтобы он мог корректно передавать голосовые команды. Подключаем провода так, как показано на схеме ниже.

![AI-Arduino](https://github.com/user-attachments/assets/ad81b926-b0ca-40cd-a8ec-6b093e6d05b8)

### 3.5 Подключение логической части к L298N
  Теперь можно подключить Arduino и голосовой модуль к драйверу. Помимо питания нам нужно будет подключить входы, которые позволят передавать команды на моторчики. На драйвере эти ходы обозначены как: IN1, IN2, IN3 и IN4.

  ![Arduino-L298N](https://github.com/user-attachments/assets/b3e9b5db-942b-4141-98c5-8d3e379b5a6b)
