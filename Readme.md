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
![1684749087634](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/66e520bd-a477-4b72-8da9-8a16e1a1c481)
*После чего можно перезагружаться и заходить в систему с новым паролем. Использовать можно ,когда  потеряли или вообще не имели пароль администратора.

*Способ 3. rw init=/sysroot/bin/sh
В строке начинающейся  с linux16 заменāем ro на rw init=/sysroot/bin/sh и нажимаем сtrl+x для загрузки системы :
![1684744480656](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/751ccc39-d3ae-4cc9-ad8f-12499e608cc8)
*Вход в систему :
![1684744440069](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/e22b6980-b713-4a0e-9918-aab9cc395da9)
*Система сразу же смонтировалась в режим Read-Write
![1684744480656](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/1c5438ca-6344-44c8-8d06-d35df9b2b5a6)

4.Установить систему с LVM, после чего переименовать VG
*Текущее состояние системы:
![1684744585620](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/33ea5e3e-e929-43bc-8dbb-cb27948bd242)
*Переименовываем VG
![1684744627100](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/40dc29ad-ef5f-44f7-be15-5e07d2c7330c)
Вносим изменения в  /etc/fstab, /etc/default/grub, /boot/grub2/grub.cfg. Везде заменяем старое значение на новое.Для редактирования используем команду vi, что бы сохранить изменения в файле вводим :wq!(что означает записать и выход)
/etc/fstab:

![1684744776154](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/6709a6af-54f1-4e36-b472-fca5f8fffbce)

![1684744748763](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/210028af-d09f-490f-aa66-75097f99689c)

![1684744818977](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/a581d46e-2cac-466e-8866-e6681832d274)

/etc/default/grub:

![1684744858776](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/b71ecc10-bc30-49ea-9882-1ff10123655d)

![1684744981187](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/c51b0523-3559-4995-ab08-06935970685b)

/boot/grub2/grub.cfg:

![1684745006338](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/ee8ec220-4539-4c1c-952b-78b3291c84e9)

![1684745094021](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/6cf074b7-6752-4093-9f59-23c023d68520)

*Пересоздаем initrd image, чтобы он знал новое название Volume Group

![1684745157658](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/e055c560-00f6-4ed0-8b6a-a128c9a8c121)

![1684745193401](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/deb3cc27-0c1c-40d1-80c0-11bc84719a19)
*После чего можем перезагружаться и если все сделано правильно успешно грузимся с новым именем Volume Group и проверяем:

![1684745210808](https://github.com/AlexanderSerg-jun/boot_system/assets/85576634/7d64619c-9300-4bd4-8deb-9a3afb5092ec)
*Добавить модуль в initrd






















