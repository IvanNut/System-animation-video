# Разработка системы автоматической анимации лиц на основе нейронных сетей и методов глубокого обучения
Этот репозиторий в основном предоставляет ориентированный на Windows графический интерфейс Radio для тренеров Kohya Stable Diffusion.

Для обучения модели мы будем использовать пользовательский интерфейс Kohya.
Для демонстрации сгенерируемого изображения мы используем Stable Diffusion.

:exclamation: Желатель иметь куда ядра
## Шаги разработки :computer:
### 1. Установка репозитория :cd:
#### Дополнительные требования для ОС Windows

Чтобы установить необходимые зависимости в системе Windows, выполните следующие шаги:

1. Установите [Python 3.10](https://www.python.org/ftp/python/3.10.9/python-3.10.9-amd64.exe). :snake:
   * При установке убедитесь, что вы выбираете опцию добавить Python в переменную среды 'PATH'.

2. Установите [Git](https://git-scm.com/download/win). :octocat:

3. Установите библиотеки [Visual Studio 2015, 2017, 2019 и 2022](https://aka.ms/vs/17/release/vc_redist.x64.exe ). :package:
   
#### Установка
Чтобы настроить проект, выполните следующие шаги:

1. Откройте терминал и перейдите в желаемый каталог для установки.

2. Клонируйте репозиторий, выполнив следующую команду:
    ```
    git clone https://github.com/bmaltais/kohya_ss.git
    ```
3. Перейдите в каталог kohya_ss:
   ```
   cd kohya_ss
   ```
4. Запустите скрипт настройки, выполнив следующую команду:
   ```
   .\setup.bat
   ```
---
После запуска программы у вас будет такой интерфейс: :arrow_down:
![mark](https://sun9-62.userapi.com/impg/yCA5GLVixGyWU1QT8d_Z8v53h_fOfC18iQLLJA/wixvyOpdxlQ.jpg?size=960x480&quality=96&sign=43c0d5de4a71aaf820a3ba79c7f77ff0&type=album)
Нужно для начала установить все необходимые библиотеки для запуска программы, поэтому выбираем первый пункт.

После того как мы установили все необходимые компоненты запускаем программу(Жмем 5 и enter).

После запуска программы у нас будет вот такой интерфейс: :arrow_down:
![xxxx](https://sun9-11.userapi.com/impg/S9dMIJ2fHgnDmFZyHKJWT7IlynPwZkNjooyZ6A/b3BpJ_fHgb8.jpg?size=1873x1003&quality=96&sign=0346fc8f26adbb4a11959fc088a1c872&type=album)

Супер, первый шаг мы выполнили

---
### 2. Модель контрольной точки :dvd:
Тут нужно уточнить, что мы не создаем заново велосипед. Наша задача дообучить модель так, чтобы наш персонаж был в этой модели и генерировался программой.

Поэтому нужно взять модель контрольной точки, чтобы в дальнейшим дообучить ее.
Для примера я взял модель [SD XL](https://civitai.com/models/101055/sd-xl)

---
### 3. Подготовка данных :scroll:
Вообще желательно чтобы создать Идеальное творение нужно подготовить качественный большой датасет. Но к сожелению у нас не было столько времени для выполнения такой задачи.

Наш датасет охватывал порядка 80 фотографий разных ракурсов(Главный Герой :guardsman: :arrow_heading_down:):
![yyyy](https://sun9-46.userapi.com/impg/HRMCn883wf62SyseYGoBYMSYg42ayLKDVe8LWg/9UFGNT0tCgw.jpg?size=1000x1000&quality=96&sign=498665ad8c06a078af10c8231c70df2b&type=album)

---
### 4. Настройка Kohya и обучение :books:
После того как все материалы были собраны, приступим к самому интересному.
#### Загрузка чекпоинта и подготовка выборок :open_file_folder:
В интерфейсе Kohya нужно загрузить наш чекпоинт:
![hhhh](https://sun9-5.userapi.com/impg/9aU10u59yLHmlmQxi42i-JS07oEhv40WDxKrGg/5fKFDJSACXA.jpg?size=1868x1004&quality=96&sign=f8c7de3b98cc8489023a5e954b5cdfa1&type=album)

Далее нужно мы переходим в раздел ***Dataset Preparation***. Здесь в Instance prompt мы указываем имя, Instance prompt - это ключевое слово, которое запускает модель Lora.

*Class prompt* - определяет тему или стиль изображения, здесь мы также указываем имя.

*Training images* - здесь мы указываем изображения(В моем случае изображения меня) для стилизации. Если вы собираетесь обучать на фотографиях людей, то фотографии должны быть идеального качества.

*Regularisation images* - регуляризация изображения, для примера если мы хотим чтобы наш персонаж был с волнистыми волосами, то нужно сюда загружать различные фотографии где есть волнистые волосы. Здесь фотографий должно быть в два раза больше чем тренировочных фотографий

Параметр *Repeats* - это число повторений в тренировочных фотографий и для регуляризаций изображений.

Далее нам нужно указать папку, где у нас будут хранится наши подготовленные данные(*Destination training directory*)

После нам нужно нажать на кнопку *Prepare training data*

И заключительное: Копировать это в Folders Tab(Нажать на кнопку *Copy info to Folders Tab*)

![lllll](https://sun9-6.userapi.com/impg/csAGdDzZYQOOU6FbKlS0zzYIaKpwPOK50H1tZQ/0ZJxjcw4BYM.jpg?size=1867x1004&quality=96&sign=e3220ee41c3f0ed49efae23e26d43b60&type=album)

---

#### Задаем будущей модели имя и то как она будет вызываться
Переходим на вкладку ***Folders*** и обращаем внимание на *Model output name* и *Training comment*

В *Model output name* указываем название модели

В *Training comment* указываем **use trigger word name_model name_person**

![vvvv](https://sun9-53.userapi.com/impg/BLQ_KYUWiDEtmuh02I9smdGPIFjVRZ12jh4QJg/tMUGthyjjZ8.jpg?size=1868x1004&quality=96&sign=9e82b3167c86b53896d6bd9264414676&type=album)

---

#### Настройка параметров и обучение :books:
Переходим на вкладку ***Parameters***. Здесь мы видим кучу всего, но нам нужно лишь некоторые параметры. Сразу скажу, что все те параметры я настраивал я настраивал для железа GTX1660 4GB. Если вы планируете увеличивать нагрузку на систему для увеличения качества модели, то я скину видеоролик, где вы полностью разберетесь с параметрами.

* **LR Scheduler** - указываем *constant*

* **Optimizer** - указываем *adafactor* :heavy_check_mark:
* ***Max resolution*** - указываем 360x640 :heavy_check_mark:
* ***Full fp16 training (experimental)*** - ставим галку :heavy_check_mark:
* ***Gradient checkpointing*** - ставим галку :heavy_check_mark:
* ***Memory efficient attention*** - ставим галку :heavy_check_mark:

После того как мы все выставили жмем на долгожданную кнопку ***Start training***
![iiii](https://sun9-2.userapi.com/impg/BJL4QFXx5oT8HyXr7rFvYLuWkZSmmT_DgdTBbg/u0BrElf0Gn4.jpg?size=1870x1003&quality=96&sign=9475664b2edddfc3d0f5049cd28932a9&type=album)

![pppp](https://sun9-12.userapi.com/impg/n5uWKC_jPRGbLV7d7d4aYze31xPk2i3O_HKKoQ/jA1GJfPSuTM.jpg?size=1871x1003&quality=96&sign=38d53c24b01b589f909905530cf9f2f4&type=album)

![oooo](https://sun9-12.userapi.com/impg/ppEuDHX2Xkv1MptzuY9GpzLXipnj6B83rCPWCQ/s0SUkeD5HlU.jpg?size=960x480&quality=96&sign=ad8d132ca2e817105d7ef6e98725e112&type=album)

После того как выша модель обучилась, она будет расположена *ControlAltAi Lora\model*

---

### 4. Демонстрация нашего творения, а именно тест модели :triangular_flag_on_post:
Как мы уже писали выше, мы будем использовать Stable Diffusion(Про установку SD говорить не будем, посколько все находится в открытом доступе)

* Запускаем SD и выбираем модель SD XL :white_check_mark:
* Далее пишем промт используя Наши ключевые слова :white_check_mark:
* И последнее мы переходим в ***Lora*** и выбираем нашу дообученную модель :white_check_mark:
* Генерируем фотку :white_check_mark:

Вот какие творения у нас получились: :rocket: :rocket: :rocket:

![poiu](https://sun9-80.userapi.com/impg/7Xm1_IQfqqFgXNFZqgQ7Qltm5vgTCLkZ-JbARA/ZXct_gPNYkI.jpg?size=1873x1004&quality=96&sign=dc0e3cb56899b9e85f088c443c52f2e6&type=album)

![yttr](https://sun9-12.userapi.com/impg/Zf38VHB2fliT52x2znfuLQHFY-GLsnlsjHv0Gw/4qYZzlQ8Ld0.jpg?size=720x1280&quality=96&sign=06e082ad8df287a0a4317700aef46521&type=album)

![nbvc](https://sun9-5.userapi.com/impg/dxCKwfzSRC1iuCdJEfufe-1hTebiUL-ngvP8vw/fTvvEZgYXlQ.jpg?size=720x1280&quality=96&sign=75aec24eab889123813c75875113a7a2&type=album)

--
## Источники :grey_exclamation: :grey_exclamation: :grey_exclamation:
Здесь мы покажем откуда брали информацию
* https://youtu.be/_F39RbO3tYo?si=WsBc8nszshcrCP4A - Stable Diffusion Lora Training with Kohya (Tutorial) :movie_camera:
* https://youtu.be/mnel2E9SFzk?si=OdqFWja1yETElFUW - Полный гайд. Тренируем Lora Stable Diffusion :movie_camera:
* https://youtu.be/xholR62Q2tY?si=eQbz-IgeQ0X71i5B - Training LoRA with Kohya (theory included!) :movie_camera:
