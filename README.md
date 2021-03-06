# Практика 2. Основы работы с библиотекой OpenCV

[![Build Status](https://travis-ci.org/Itseez-NNSU-SummerSchool2015/practice2-opencv-intro.svg)](https://travis-ci.org/Itseez-NNSU-SummerSchool2015/practice2-opencv-intro)

## Цели

__Цель данной работы__ - изучить базовые примитивы модуля `opencv_core`
и простейшие операции обработки изображений модуля `opencv_imgproc`, научиться
разрабатывать интерфейс средствами модуля `opencv_highgui`.

Проект представляет собой шаблон проекта для освоения основ работы
с библиотекой OpenCV:

  - Базовые примитивы и операции модуля `opencv_core`
    (методы класса `cv::Mat` для представления изображения).
  - Обработка изображений с помощью простеших фильтров модуля `opencv_imgproc`
    (линейные фильтры, вычисление градиентов на изображении).
  - Основные операции модуля `opencv_highgui` (загрузка изображения
    средствами `imread`, сохранение изображения с использованием
    `imwrite`, отображение изображения с помощью функций `imshow` и `waitKey`,
    реализация сложных сценариев обработки событий).

## Общая структура проекта

Структура проекта:

  - `sample_template` - исходные коды шаблонного проекта. Шаблонное
    приложение отображает исходное изображение и изображение, полученное в
    результате медианной фильтрации центральной части исходного изображения.
    Также в окне имеется 2 кнопки, позволяющие включить/отключить действие
    фильтра.
  - `testdata` - директория с данными для тестов.
  - `.gitignore` - перечень расширений файлов, которые не выкладываются в
    проект.
  - `.travis.yml` - конфигурационный файл для системы автоматического
    тестирования Travis-CI.
  - `CMakeLists.txt` - общий файл для сборки проекта с помощью CMake.
  - `README.md` - информация о проекте, которую вы сейчас читаете.

В шаблонном проекте имеются следующие модули:

  - Основной модуль `main`, содержащий реализацию основного сценария работы
    шаблонного приложения: разбор аргументов командной строки, чтение кадра,
    ожидание нажатия на кнопки и обновление состояния окна с изображениями.
  - Модуль `processing` содержит метод медианной фильтрации центральной области
    изображения.
  - Модуль графичекого приложения `application`. Содержит метод обработки
    аргументов командной строки `parseArguments`; обертку `processFrame` над
    функцией обработки изображения с использованием метода, реализованного в
    модуле `processing`; метод отображения окна с двуми изображениями - исходным
    и обработанным, если фильтр включен, либо двумя исходными, если фильтр
    выключен; методы, необходимые для обработки событий нажатия на кнопки
    включение/выключения фильтра.

## Задачи

__Основные задачи:__

  1. Обеспечить возможность изменения положения региона фильтрации со временем
     (траектория движения может быть выбрана произвольным образом, например,
     движение по диагонали, движение по диагонали с отражением, случайное
     изменение положения и другие).
  2. Добавить третью кнопку, чтобы обеспечить возможность сохранения текущего
     изображения окна.
  3. Добавить несколько дополнительных кнопок, позволяющих изменять тип фильтра:
     - Перевод центральной части изображения в оттенки серого вместо медианной
       фильтрации.
     - Поддержка режима пикселизации центральной области изображения (подобно
       тому, как на телевидении скрывают лицо человека).
     - Применение Канни детектора для определения ребер в центральной части
       исходного изображения.

__Дополнительные задачи:__

  1. Реализовать возможность получения кадров из видеофайла и/или камеры.
  2. Реализовать случайное перемешивание картинки как в игре в "пятнашки".
  3. Реализовать приложение для игры в пятнашки.

## Общая последовательность действий

  1. Сделать форк upstream-репозитория, затем клонировать origin к себе на
     локальную машину. Для инструкций можно обратиться к разделу
     [Общие инструкции по работе с Git][git-intro] в [практической работе 1][practice1].
  2. Скомпилировать и запустить сэмпл на картинке (раздел
     [Сборка проекта с помощью CMake и MS VS][cmake-msvs]
     в [практической работе 1][practice1].
  3. Создать новую ветку для разработки собственного приложения
     необходимые команды описаны в разделе
     [Общие инструкции по работе с Git][git-intro] в [практической работе 1][practice1].
  4. Создать копию директории с сэмплом, добавить ее построение в корневой
     `CMakeLists.txt`.
  5. Убедиться, что новый сэмпл успешно собирается и запускается.
  6. Прислать Pull Request с еще неизмененным сэмплом. Пометить в конце названия
     `(NOT READY)`. По мере готовности решений основных задач Pull Request можно
     будет переименовать.
  7. Сделать так, чтобы регион фильтрации менял со временем свое положение и
     размеры. Обновить Rull Request.
  4. Добавить третью кнопку, позволяющую сохранить текущее изображение на
     экране. Сохранять можно в текущую директорию с меткой времени. Обновить
     pull request.
  5. Добавить несколько дополнительных кнопок, позволяющих менять тип фильтра
     (см. перечень ниже) и обновить Rull Request.
     - Простой перевод в оттенки серого (функция [cvtColor][cvtColor].
     - Режим пикселизации (подробнее можно прочитать [здесь][pixelation].
     - Режим применения Канни детектора (пример использования функции
       [Canny][canny].
  6. Решить задачи из списка [Дополнительные задачи][tasks] (документация к
     классу [cv::VideoCapture][capture] для работы с видео).

## Детальная инструкция по выполнению работы

  1. Сделать форк upstream-репозитория и клонировать origin к себе на локальную
     машину (подробная последовательность действий описана в разделе
     [Общие инструкции по работе с Git][git-intro] в [практической работе 1][practice1].
  2. Скомпилировать и запустить сэмпл на картинке (подробная последовательность
     действий описана в разделе [Сборка проекта с помощью CMake и MS VS][cmake-msvs]
     в [практической работе 1][practice1]).
  3. Создать новую ветку для разработки собственного приложения
     необходимые команды описаны в разделе
     [Общие инструкции по работе с Git][git-intro] в [практической работе 1][practice1].
  4. Создать копию директории с сэмплом, дав ей название `sample_YOUR_NAME`, и
     добавить ее построение в общий `CMakeLists.txt`
     (`add_subdirectory(sample_YOUR_NAME)`). В файле `CMakeLists.txt`, отноящемся
     к созданному проекту (расположен внутри директории `sample_YOUR_NAME`)
     необходимо заменить `set(target "sample_template")` на
     `set(target "sample_YOUR_NAME")`
  5. Убедиться, что новый сэмпл с шаблонной реализацией успешно собирается
     и запускается (подробная последовательность действий описана в разделе
     [Сборка проекта с помощью CMake и MS VS][cmake-msvs]
     в [практической работе 1][practice1]).
  6. Прислать Pull Request с еще неизмененным сэмплом. Пометить в конце
     названия `(NOT READY)`. По мере готовности решений основных задач Pull
     Request можно будет переименовать, нажав кнопку `Edit` напротив его
     названия.
  7. Сделать так, чтобы регион фильтрации менял со временем свое положение и
     размеры.
     1. Для этого необходимо в методе `processFrame` класса `Processing`
        заменить фиксированное положение фильтра на процедурную генерацию
        положения левого верхнего угла `x` и `y` региона `region` при
        фиксированных размерах окна фильтрации. Положение окна может выбираться
        случайно, или по некоторому закону (например движение по прямой линии с
        отражением от краев изображения).

     ```
     cv::Rect region(src.rows/4, src.cols/4, src.rows/2, src.cols/2);
     ```

        При генерации следует учитывать, что окно фильтрации должно попадать в
        область изображения. Решение 1: пределы генерации координат должны быть
        зафиксированы так, чтобы окно всегда накрывало какую-то часть
        изображения. Решение 2: проверять, не вышло ли окно за пределы
        изображения, если вышло, то обрезать лишние части окна.
     2. Не забывайте коммитить изменения в локальный репозиторий и выкладывать
        их в ветку на сервере.
     3. По окончании решения данной задачи следует обновить Rull Request.
  8. Добавить третью кнопку, позволяющую сохранить текущее изображение на
     экране. Сохранять можно в текущую директорию с меткой времени.
     1. В структуру `GUIElementsState` (файл `Application.hpp`) добавить поле
        `cv::Rect saveButtonPlace`.
     2. В метод `drawButtons` класса `Application` добавить отрисовку третьей
        кнопки по аналогии с кнопками включения/выключения фильтрации.
        Расположить кнопку необходимо на одной линии с имеющимися. Также на
        кнопке следует добавить надпись `Save`. Положение кнопки сохранить в
        поле `saveButtonPlace` объекта `guiState`.
     3. В структуру `GUIElementsState` добавить поле `bool saveState` - флаг,
        обозначающий необходимость сохранения текущего окна с изображениями.
        Изначально присвоить ему значение `false` в конструкторе класса
        `Application`.
     4. В реализацию метода `onButtonsOnOffClick` добавить еще одно условие для
        обработки события, связанного с нажатием кнопки сохранения.

     ```
     if (onButtonClicked(elems->saveButtonPlace, x, y))
     {
        elems->saveState = true;
        return;
     }
     ```

     5. В реализацию метода `showFrame` класса `Application` после отрисовки
        пары изображений и до отрисовки кнопок необходимо вставить условие для
        проверки необходимости сохранения текущей пары изображений.

     ```
     if (elems->saveState)
     {
        // получить текущее время
        // сгенерировать название изображения
        // <image_name> - сгенерированное название изображения
        //                с меткой текущего времени
        // вызвать функцию сохранения imwrite(<image_name>, display)
        // сбросить значение guiState.saveState в false
     }
     ```

     6. Обновить Pull Request.

  9. Добавить несколько дополнительных кнопок, позволяющих менять тип фильтра
     (см. п.3 раздела [Основные задачи][tasks].

     1. В класс `Processing` добавить перечисление для обозначения типа фильтра,
        который применяется к изображению.

     ```
     enum FilterType
     {
         MEDIAN,
         CVT_CONVERT_GRAY,
         PIXELIZED,
         CANNY
     };
     ```

     2. В объявление метода `processFrame` класса `Processing` добавить параметр
        типа `FilterType filter`.
     3. В реализации метода `processFrame` класса `Processing` вместо вызова
        функции медианной фильтрации `medianBlur(roi, roi, kSize)` добавить
        оператор множественного выбора по параметру `filter`. В зависимости от
        типа фильтра необходимо вызывать тот или набор функций библиотеки
        OpenCV.
     4. Отрисовать дополнительные кнопки по аналогии с кнопкой сохранения
        изображений. Положение кнопок сохранить в структуре `GUIElementsState`.
        Замечание: кнопку `On` можно только переименовать в `Median`.
     5. В структуру `GUIElementsState` добавить поле для хранения типа
        последнего вызванного для обработки фильтра `Processing::FilterType
        filter`.
     6. В конструкторе класса установить начальное значение `guiState.filter` в
        значение `Processing::MEDIAN`.
     7. Вызов метода `processor.processFrame(src, dst)` заменить на
        `processor.processFrame(src, dst, guiState.filter)` (метод класса приложения
        `int Application::processFrame(const Mat& src, Mat& dst)`).
     8. Изменить обработчик события нажатия по кнопкам `onButtonsOnOffClick`,
        добавив несколько проверок, соответствующих нажатию по определенным
        кнопкам. Содержимое условного оператора приведено ниже.

     ```
     elems->state = Application::OnFilter;
     elems->filter=Processing::MEDIAN;
     return;
     ```

     9. Проверить работоспособность приложения и обновить Rull Request.
  10. Решить задачи из списка [Дополнительные задачи][tasks].

<!-- LINKS -->

[practice1]: https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools
[git-intro]: https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools#Общие-инструкции-по-работе-с-git
[cmake-msvs]: https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools#Сборка-проекта-с-помощью-cmake-и-microsoft-visual-studio
[tasks]: https://github.com/Itseez-NNSU-SummerSchool2015/practice2-opencv-intro#Задачи

[cvtColor]: http://docs.opencv.org/modules/imgproc/doc/miscellaneous_transformations.html#cvtcolor
[pixelation]: http://opencv-code.com/tutorials/photo-to-colored-dot-patterns-with-opencv
[canny]: http://docs.opencv.org/doc/tutorials/imgproc/imgtrans/canny_detector/canny_detector.html
[capture]: http://docs.opencv.org/modules/highgui/doc/reading_and_writing_images_and_video.html#videocapture
