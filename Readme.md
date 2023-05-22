Попасть в систему без пароля несколькими способами.
Для получения доступа необходимо открываем GUI VirtualBox! 
Запуститим виртуальную машину. 
![1684743032094](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/3c399f01-20e5-4af1-a790-1d1c9eddeba2)

*При выборе ядра для загрузки нажмем e. Попадаем в меню параметров загрузки
![1684743066007](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/80d97456-cb1c-4c25-8dd5-f99631bf97ce)


Способ 1. init=/bin/sh
*Находим строку, которая начинается с с linux16, добавляем в конце строки "init=/bin/sh" и нажимаем сtrl-x для загрузки  системы
![1684743278472](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/566dcdb8-c2d5-48d5-b95e-512127644b4f)

*Попадаем в систему без пароля
![1684743299127](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/c5e646c0-07d7-4e7b-a166-1733bd190e58)

*Рутоваā файловая система монтируется в режиме Read-Only. Если нам  необходимо перемонтировать ее в режим Read-Write можно воспользоваться командой: mount -o remount,rw/ и проверим сразу смонтировалась ли система в режиме Read-Write, используем команду c конвеером mount |grep root

![1684743536399](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/7ee78009-645a-4619-b00b-fcbd0adc1466)
 Способ 2. rd.break
 *Находим строку, которая начинается с с linux16, добавляем в конце строки "rd.break" и нажимаем сtrl-x для загрузки  системы
 ![1684743609124](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/b674f4f5-d733-427c-a812-e3240f7a035f)
 *Попадаем в систему
![1684743630301](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/dc94af0c-37ab-4742-b411-cbc34c2034cf)
*Попадаем в emergency mode. Файловаā система смонтирована (в режиме Read-Only), но мы не в ней.
![1684743655886](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/7011de62-2dcb-489e-9a08-258cab96340a)

*Используем команду mount -o remount,rw /sysroot ( монтируем систему в режиме Read-Write).
![1684744259886](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/c88b6e5f-a057-4b2c-ac2f-4fd6e651ce52)
*далее используем команду chroot /sysroot (Операция изменения корневого каталога в Unix-подобных операционных системах)
![1684744291772](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/13f7d238-601c-4189-bc2e-a74ea2d90cf8)
*Используя команду passwd root меняем пароль root'а. Так был использован слабый пароль то система нас об этом предупреждает
![1684744326762](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/be541ff7-0c6b-40cb-aaf9-6afbb59e1346)
*После чего используем команду touch /.autorelable (Команда создает скрытый файл с именем .autorelabel в корневом каталоге. При следующей загрузке подсистема SELinux обнаружит этот файл, а затем повторно пометит все файлы в этой системе правильными контекстами SELinux.)
