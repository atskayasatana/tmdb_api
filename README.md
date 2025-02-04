### Упражнение на чтение кода. Фильмы с TMDB

Приложение для поиска фильмов в базе TMBD. 

Для начала работы необходим Python 3 и ряд бибилиотек, которые указаны в файле зависимостей requirements.txt. 
Архив с приложением нужно скачать и распаковать в любую директорию на своем компьютере. После этого можно запустить командную строку, перейти в директорию проекта (команда cd) и установить нужные библиотеки:

```
pip install requirements.txt
```

Любой из скриптов в проекте запускается в директории проекта командой ниже:
```
python имя скрипта
```


## Основные функции и скрипты

### find_similar.py

```
python find_similar.py
```
Отображает рекомендованные для пользователя фильмы.

Пользователю предлагается ввести путь к базе данных и фильм для поиска.
Если путь указан правильно, то пользователь может ввести название фильма для поиска, в противном случае появляется сообщение об ошибке "File not found, sorry...".
Если пользователь указал фильм, которого нет в базе, то появляется сообщение 'No such film in FilmsDB'.
Когда все данные введены правильно, то пользователь получает список рекомендованных к просмотру фильмов, которые имеют такие же: бюджет, жанр, язык и коллекцию.

Функции:

#### def find_my_film(keyword, films_data)

Проверяет есть ли фильм с азванием keyword в базе данных films_data. 
Если фильм найден, то возвращает фильм.

#### def get_rating(my_film, films_data, num_to_recommend=8)

Возвращает 8 рекомендованных к просмотру фильмов. Ранжирование осуществляется по параметрам фильма: сравниваем параметры my_film и фильма из базы данных films_data,
каждый совпадающий параметр увеличивает ранг фильма( чем больше параметров my_film и любого фильма совпали, тем выше рейтинг). 8 фильмов с самым высоким рейтингом
показываем пользователю.

### hello_api_TMDB.py
```
python hello_api_TMDB.py

```
Возвращает бюджет фильма с номером 215.

Пользователь должен ввести свой api_key. Если ключ корректный, то на экране появится бюджет фильма с номером 215.
Если ключ введен неверно, то увидим сообщение об ошибке 'Invalid api key'

### make_own_db.py
```
python make_own_db.py
```

Функция выгружает фильмы из базы в файл пользователя в формате JSON.

Пользователь должен ввести свой api_key.
Если ключ введен неверно, то увидим сообщение об ошибке 'Invalid api key'.
Если ключ корректный, то подключаемся в базе и выгружаем фильмы. 
Пока идёт загрузка на экране отображается строка состояния с % выполнения.

#### def load_films(user_api_key, films_amount=1000)

Возвращает список словарей с данными о фильмах с id от 0 до films_amount для пользователя с user_api_key. 
Если фильм не найден, то никаких сообщений об ошибке не выводим, продолжаем загрузку.


### own_db_helpers.py

Библиотека с функцией для преобразования JSON-файлов в словарь

#### def load_data(path)

Функция получает на вход путь к файлу. Если путь указан верно, то содержимое файла конвертируется в объект типа словарь.


### search_in_db.py

```
python search_in_db.py
```

Поиск фильмов по ключевому слову. 

Пользователю предлагается ввести путь к базе данных, если путь указан неверно,появляется сообщение об ошибке "File not found, sorry...".
Если путь к базе указан верно, то пользователь может задать ключевую фразу для поиска. Сравнение осуществляется по названиям фильмов.

#### def search_for_film(keyword, films_data)

Для каждого фильма из films_data проверяем содержит ли его название подстроку keyword.
Все удовлетворяющие этому условию фильмы попадут в результат поиска.

### tmdb_helpers.py

Библиотека с функциями для работы с запросами к базе данных

#### def load_json_data_from_url(base_url, url_params)

Функция получает на вход адрес сервера base_url и параметры запроса url_params.Затем с помощью функционала библиотеки urllib преобразует 
эти данные в url для запроса. 
Возвращает JSON файл с результатом запроса.


#### def make_tmdb_api_request(method, api_key, extra_params=None)

На вход получает ключ пользователя, метод запроса и дополнительные параметры(по умолчанию None), возвращает JSON файл с результатом запроса.
Для формирования url запроса использует функцию load_json_data_from_url(base_url, url_params).

#### def get_user_api_key()

Запрашивает у пользователя ключ. С данным ключом отправляет запрос к базе данных. Для отправки запроса используется make_tmdb_api_request.
Если при запросе возникли проблемы с аутентификацией, то функция ничего не возвращает. 
В противном случае, функция вернёт введенный пользователем ключ.
























