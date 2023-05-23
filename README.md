# Микропрограммый управляющий автомат

Реализация и симулаяция управляющего автомата с принудительной адресацией в паре с операционным автоматом [КМ1804](http://dplm2008.narod.ru/str/komplects/km1804/km1804vs1.html). Реализованный автомат не является тьюринг-полным. Из памяти имеет только регистровый файл, микропрограммную память и программную память. 

## Задача

Далее РОН - регистр общего назначения

1. Реализовать микропрограммный автомат с принудительной адресацией с оптимальным для выполнения следующей задачи набором инструкций. 
2. Разработать микропрограмму, которая выполняет операции с разрядами РОНi и РОНj, нумерация разрядов регистров i и j – сквозная: определяет разряды с 0 в коде регистров РОНi и РОНj и записывает произвольное число А в регистры с номерами, соответствующими номерам единичных разрядов (РОНi и РОНj).
3. Релизовать аппаратный умножитель 4x4 и произвести на нем умножение произвольных чисел


### Решение задачи 1. Принудительная адресация

В управляющем автомате, использующем принудительную адресацию, в отличие от естественной, переход происходит на каждой инструкции по одному из двух указанных адресов. Если необходимо, чтобы программа выполнялась последовательно, необходимо для каждой инструкции в качестве одного из 2 указываемых адресов перехода явно указывать адрес следующей инструкции в памяти и выбирать соответствующую функцию перехода.

 По классификации Дэвида М. и Сары Л. Харрисов, приведенной в книге "Цифровая схемотехника и архитектура компьютера. RISC-V" реализованный автомат является неполной версией многотактного процессора. Каждая инструкция реализуется набором микрокоманд, хранящихся в микропрограммной памяти в ПЗУ. Каждая инструкция выполняется переменное число тактов.

 Итоговая тактовая частота ~1.2 Мгц. Критический путь проходит через умножитель (матричный).

[Функциональная схема УА с принудительной адресацией](./img/fafuncschema.PNG)

### Решение задачи 2

Для решения задачи был разработан набор инструкций (\<d\> - imm\[4:0\] (Значение), \<b\> - addr\[4:0\] (Адрес регистра)):

[Набор инструкций](./img/istable.PNG)

### Решение задачи 3

Для решения задачи был выбран матричный умножитель ввиду простоты его реализации

[Матричный умножитель](./img/mult.PNG)

### Запуск симуляции

1. Для симуляции работы необходим Proteus версии 8.13 и выше. Так же необходим MS Visual Studio build tools для корректрного подключения динамической библиотеки. 
2. Приложенную библиотеку MT1804.dll необходимо скопировать в директорию установки Proteus в поддиректорию BIN. 
3. Запустить проект MPA_PA_v3.1.pdsprj и запустить симуляцию в левом нижнем углу.
4. В результате симуляции на внешнем устройстве, состоящем из 8 регистров должны появиться определенные значения. 
