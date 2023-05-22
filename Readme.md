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
