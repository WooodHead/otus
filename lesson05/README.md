## Домашнее задание.Работаем с процессами.

### Цель:
  В результате ДЗ вы разберетесь что находится в файловой системе /proc
и закрепите навыки работы с bash. Зачастую, например в контейнерах, у
вас нет кучу удобных утилит предоставляющих информацию о процессах, ip
адресах, итд И есть только один инструмент bash и /proc.  

### Задания на выбор:
1) написать свою реализацию ps ax используя анализ /proc
    - Результат ДЗ - рабочий скрипт который можно запустить
2) написать свою реализацию lsof
    - Результат ДЗ - рабочий скрипт который можно запустить
3) дописать обработчики сигналов в прилагаемом скрипте, оттестировать, приложить сам скрипт, инструкции по использованию
    - Результат ДЗ - рабочий скрипт который можно запустить + инструкция по использованию и лог консоли
4) реализовать 2 конкурирующих процесса по IO. пробовать запустить с разными ionice
    - Рзультат ДЗ - скрипт запускающий 2 процесса с разными ionice, замеряющий время выполнения и лог консоли
5) реализовать 2 конкурирующих процесса по CPU. пробовать запустить с разными nice
    - Результат ДЗ - скрипт запускающий 2 процесса с разными nice и замеряющий время выполнения и лог консоли 

# Домашняя работа.

### Цель:
  Разобраться в файловой системе /proc и работе с приоритетами процессов.  

### Домашнее задание №1
  1) написать свою реализацию ps ax используя анализ /proc  
  #### решение:
  скрипт psax.sh, реализующий команду 'ps ax'

### Домашнее задание №4
  4) реализовать 2 конкурирующих процесса по IO. пробовать запустить с разными ionice  
  #### решение:
  скрипт io.sh, реализующий конкуренцию по io. Запуск скрипта осуществляется командой 
(sh io.sh A&);(nice -n 19 sh io.sh B&). Ниже приведен вывод работы, а так же приложен 
вывод top в [io_top.png](https://github.com/alexshangin/otus/blob/master/lesson05/io_top.png)
  #### вывод:
  как видно из времени обработки значение nice играет большую роль в распределении
приоритетов ресурсов при одновременном их использовании.

[root@otuspsax vagrant]# (sh io.sh A&);(nice -n 19 sh io.sh B&)

[root@otuspsax vagrant]#

2048+0 records in

2048+0 records out

2147483648 bytes (2.1 GB) copied, 16.7609 s, 128 MB/s


real	0m17.241s

user	0m0.000s

sys	0m14.949s


2048+0 records in

2048+0 records out

2147483648 bytes (2.1 GB) copied, 44.1511 s, 48.6 MB/s


real	0m44.658s

user	0m0.000s

sys	0m16.208s


### Домашнее задание №5
  5) реализовать 2 конкурирующих процесса по CPU. пробовать запустить с разными nice  
  #### решение:
  скрипт cpu.sh, реализующий конкуренцию по io. Запуск скрипта осуществляется
командой (sh cpu.sh 5000000 A&);(nice -n 19 sh cpu.sh 5000000 B&). Ниже приведен вывод
работы, а так же приложен вывод top в [cpu_top.png](https://github.com/alexshangin/otus/blob/master/lesson05/cpu_top.png)
  #### вывод:
  как видно из времени обработки значение nice играет большую роль в распределении
приоритетов ресурсов при одновременном их использовании.

[root@otuspsax vagrant]# (sh cpu.sh 5000000 A&);(nice -n 19 sh cpu.sh 5000000 B&)

[root@otuspsax vagrant]#

real	1m1.424s

user	0m52.592s

sys	0m7.913s


real	2m0.198s

user	0m51.115s

sys	0m8.515s
