
## Физическая симуляция модели организма Caenorhabditis elegans

![Фото окна с работающим симулятором](https://raw.github.com/crystalline/C-Elegans-simulator/master/img/img0.png)

Это - физический симулятор организма похожего на нематоду C.Elegans.
Цель проекта - демонстрация поведения аналогичного поведению моделируемого живого организма (хемотаксис, фототаксис, разные режимы движения).

Физическая модель представляет собой систему точечных масс и пружин с вязким анизтропным трением относительно поверхности. Уравнения динамики Ньютона интегрируются с шагом 10 миллисекунд.
Мышцы модлируются как полосы из пружин которые могут менять свою равновесную длину в зависимости от подаваемого на них сигнала возбуждения.

Пока что в качестве возбуждающего сигнала используется жёстко заданная синусоидальная функция, на следующем этапе будет подключена искусственная нервная система.
Цветовая схема: Зелёный - контакт с поверхностью, Синий - расслабленная мышечная клетка, Красный - напряжённая мышечная клетка.
Управление: стрелки вращают камеру, W,A,S,D - перемещение в плоскости XY, Q,E - перемещение по оси Z, F1 и F2 - увеличение, пробел - пауза.

### Запуск
Симулятор написан на языке Common Lisp, для запуска понадобится реализация CL (разработка производится на SBCL, но и на Clozure CL успешно проводились тесты) а также библиотеки Lispbuilder-SDL и Lispbuilder-SDL-gfx. Симулятор кроссплатформенный, тестировался на 32- и 64-битных реализациях CL на ОС Linux и Windows, главное чтобы были доступны используемые библиотеки и DLL для них.

Установка SBCL в ОС Debian и Ubuntu производится просто:

	sudo apt-get install sbcl

Самый простой способ установки библиотек - установка через [Quicklisp](http://www.quicklisp.org/beta/). Quicklisp устанавливается вот так:

	wget http://beta.quicklisp.org/quicklisp.lisp
	sbcl --load quicklisp.lisp
	
Далее запускаем sbcl в той же консоли и набираем в REPL:
	
	(quicklisp-quickstart:install)
	(ql:add-to-init-file)
	(quit)

Заметьте что для установки остальных библиотек в системе должны быть доступны DLL библиотеки SDL и SDL-gfx, обычно в Debian-подобных ОС (в т.ч. Ubuntu) их можно утсановить командой

    sudo apt-get install libsdl1.2-dev libsdl-gfx1.2-dev 

После установки Quicklisp установите библиотеки, набрав в REPL вашей лисп-системы

    (ql:quickload "lispbuilder-sdl")
    (ql:quickload "lispbuilder-sdl-gfx")

Компиляцию симулятора удобно производить через [ASDF](http://common-lisp.net/project/asdf/), предположим что симулятор находится в папке /path/to/wormsim

    (push (pathname "/path/to/wormsim/") asdf:*central-registry*)
    (asdf:load-system :wormsim)

Теперь симулятор скомпилирован и его можно запустить:

	(wormsim:start-sim)

И остановить

	(wormsim:stop-sim)

### Видео
http://vimeo.com/66661947

### Литература
1. "Towards a virtual C. elegans: A framework for simulation and visualization of the neuromuscular system in a 3D physical environment"
2. "На пути к виртуальному организму под управлением цифровой копии его нервной системы: результаты и перспективы для нематоды С. Elegans" http://litcey.ru/informatika/28911/index.html

### This is a physical simulation of C.Elegans-like nematode (worm).

;Controls: arrows for camera rotation, w a s d for movement in XY plane,
;q e for moving in Z axis, F1, F2 for zoom, space for pause

;I'll translate docs to English later
