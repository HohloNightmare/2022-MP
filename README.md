# 2022-MP,
ННГУ, курс "Методы программирования" 2022г.

Презентация по курсу (обновляемая): https://docs.google.com/presentation/d/1wmYjy5QDoYECEHi7NAAINPulU9pLsaIi-aLaUppspps/edit?usp=sharing

Для работы необходим python 3.9 и выше. Библиотеки: numpy, pandas, matplotlib, tensorflow, Pillow, scipy.signal. Редактор любой. Из неплохих: IDLE (родной, идёт вместе с установщиком), Visual Studio Code, notepad++, PyCharm, vim (для любителей сначала страдать, потом наслаждаться).

Работа с блокнотами онлайн, с возможностью подключения удалённых мощностей гугла (GPU, TPU): https://colab.research.google.com/

Таблица, где я буду отмечать сданные работы: https://docs.google.com/spreadsheets/d/1ukuncwEtZQ2gwp6FhGD3waF9M96D4eBTSghJeSzotjg/edit?usp=sharing

Сервер в Дискорд, где буду дублировать: https://discord.gg/MzPkCYf4Dh (получить роль в канале "Основной") Мой контакт: nsmorozov@rf.unn.ru

В своей папке можете делать все что угодно, в чужие не залезать, в корневую тоже. Я буду ориентироваться на файлы, где в названии будет номер лабораторной.

## Практика 1 (императивное и структурное программирование)

1. Используйте скрипт gen_lab_origin.py из папки  \_lab-1, запустите и заберите в свою папку сгенерированный лабиринт, в котором точка входа на верхней границе, а точка выхода - на нижней. 
2. Ввести с клавиатуры точку (указать в каких пределах) расположения "сокровища", найти к нему путь (любой, поиск в глубину). 
3. От точки сокровища узнать длину кратчайшего пути (поиск в ширину) к выходу (вывести) и построить его. 
4. Сохранить в файл 'maze-for-me-done.txt', в котором точка сокровища будет указана как \'\*\', а сам маршрут построен точками к сокровищу и запятыми от него к выходу.

## Практика 2 (объектно-ориентированное программирование)

0. ВАЖНО! В первую очередь, это работа по построению объектно-ориентированной архитектуры, и только во вторую - работающий код. Начните с создания классов с пустыми методами-заглушками, посмотрите как они будут взаимодействовать, какие данные каждому для работы нужны, раскидайте внутри классов поля, сделайте конструкторы. И только после того, как у вас будет готовый скелет (еще раз, БЕЗ наполнения методов и БЕЗ фактической работы, достаточно написать в каждом *print('Generator->signal')*,  т.е. писать что за метод и какого класса вызывается. И только после того, как вам окончательо станет понятно что за чем следует и как это выстроить, начинайте наполнять кодом.

1. Проект по моделированию прохождения сигнала через цепь должен содержать каждый отдельный класс в своем файле.
2. Класс генератора простых сигналов имеет функционал:
    
    - создания сигнала каждой из заданных форм: гармонический, треугольный, ШИМ с заданной скважностью, пила;
    - параметры: частота (период), частота дискретизации, длительность (как в сэмплах, так и в секундах), амплитуда;
    - возвращать как весь сигнал (всю длительность в виде массива), так и отдельную его выборку по номеру сэмпла или по отметке времени (во втором случае - ближайшую);
    - иметь функцию-генератор, возвращающий по запросу следующую выборку сигнала (yield).
    
3. Класс-наследник генератора простых сигналов, содающий амлитудно-моделированный сигнал:
    - огибающая задана в виде заранее заданного набора выборок (цифровой сигнал) с указанной частотой дискретизации этих выборок;
    - частота модулирующего сигнала или задается, или автоматически подбирается (по умолчанию можно уменьшать частоту огибающей в 20 раз относительно заполнения);
    - возвращать как весь сигнал (всю длительность в виде массива), так и отдельную его выборку по номеру сэмпла или по отметке времени (во втором случае - ближайшую);
    - иметь функцию-генератор, возвращающий по запросу следующую выборку сигнала (yield).

4. Класс анализатора сигнала должен:
    - строить график по полученному временнОму представлению сигнала;
    - строить его спектр Фурье;
    - возвращать дисперсию, среднее, медианное, минимальное и максимальное значения, размах сигнала, отображать по запросу их в виде горизонтальных линий на графике;
    - строить примерный (прогнозируемый) сигнал с помощью обратного преобразования Фурье, используя первые несколько максимальных гармоник (частот) спектра Фурье (по умолчанию - 5, но можно задать любое).

5. Класс цепи должен уметь работать как с сигналом в виде массива, так и с последовательно приходящими выборками (из методов-генераторов yield):
    - пропускать сигнал без изменений (bypass);
    - преобразовывать его указанным в п.6 алгоритмом;
    - хранить входной и выходной сигналы в буфере (заполнять массив), по умолчанию - без ограничения размера (весь), но с возможностью этот размер задать (хранить только последние пришедшие и ушедшие);
    - возвращать как полным массивом, так и генератором yield.

6. Номер конкретно вашего задания получаете из вашего ФИО следующим образом: len("Морозов Никита Сергеевич")%5 = *ваш номер задания*:


    0- свертка (convolve) сигнала с гармоническим, заданной амплитуды и частоты;
    
    1- свертка (convolve) сигнала с пилообразным (sawtooth), заданной амплитуды и частоты;
    
    2- свертка (convolve) сигнала с прямоугольным (square), заданной амплитуды и частоты;
    
    3- прохождение сигнала через фильтр Баттерворта (butter) с частотой среза (по умолчанию 0.4) и заданного порядка N (по умолчанию 4);
    
    4- прохождение сигнала через фильтр Бесселя (bessel) с частотой среза (по умолчанию 0.4) и заданного порядка N (по умолчанию 4);
    
 ## [3] Практика 3 (функциональное программирование)
 
 Реализовать в функциональной парадигме приближенное вычисление корней уравнения f(x) с заданной (с клавиатуры при запуске) точностью epsilon. Вариант задания рассчитывается аналогично предыдущему.
 
   0- ![](https://latex.codecogs.com/svg.image?\bg{black}{\color{red}&space;\ln{x}&plus;(x&plus;1)^3=0) методом касательных
   
   1- ![](https://latex.codecogs.com/svg.image?\bg{black}{\color{red}&space;(2-x)e^{x}=0) методом половинного деления
   
   2- ![](https://latex.codecogs.com/svg.image?\bg{black}{\color{red}&space;x^2=\ln(x&plus;1)) методом простых итераций
   
   3- ![](https://latex.codecogs.com/svg.image?\bg{black}{\color{red}&space;\lg(1&plus;2x)=2-x) методом хорд
   
   4- ![](https://latex.codecogs.com/svg.image?\bg{black}{\color{red}&space;2sin&space;x-arctg&space;x=0) на промежутке (2.5, 2.6) методом простых итераций
