Работа с mdadm.

Цель:

Системный администратор обязан уметь работать дисковой подсистемой,
делать это без ошибок, не допускать потерю данных. В этом задании 
необходимо продемонстрировать умение работать с software raid и
инструментами для работы с работы с разделами(parted,fdisk,lsblk):
-добавить в Vagrantfile еще дисков
-сломать/починить raid
-собрать R0/R5/R10 - на выбор
-создать на рейде GPT раздел и 5 партиций

в качестве проверки принимаются:
-измененный Vagrantfile
-скрипт для создания рейда

* доп. задание - Vagrantfile, который сразу собирает систему с подключенным рейдом


Домашняя работа 2. Цель - написание скрипта провиженинга
виртуальной машины для автоматической сбоки и подключения массива

Vagrant file - конфигурационный файл с указанием скрипта провиженинга

script_raid.sh - скрипт провиженинга вм для автоматической сборки и подключения
		 во время первичной сборки вм 