# Neobis_DjangoGirls_Project

Использовать отдельную директорию djangogirls в домашнем каталоге:


$ mkdir djangogirls
$ cd djangogirls
создали виртуальное окружение под именем myvenv. В общем случае команда будет выглядеть так:


$ python3 -m venv myvenv

Перед этим мы должны удостовериться, что у тебя установлена последняя версия pip — программы, которую мы используем для установки Django.


(myvenv) ~$ python3 -m pip install --upgrade pip

Установка библиотек через указание требований
Файл с требованиями (requirements) хранит список зависимостей, которые нужно установить с помощью pip install:

Для начала создай файл requirements.txt внутри директории djangogirls/, используя текстовый редактор, который ты установила ранее. Просто создай в редакторе новый файл, а затем сохрани его под именем requirements.txt в директории djangogirls/. После этого твоя директория будет выглядеть так:

djangogirls
└───requirements.txt
В файл djangogirls/requirements.txt нужно добавить такой текст:

djangogirls/requirements.txt
Django~=3.2.10
Теперь выполни команду pip install -r requirements.txt, чтобы установить Django.

создать новый проект Django
django-admin startproject mysite .

django-admin.py — это скрипт, который создаст необходимую структуру директорий и файлы для нас. Теперь у твоего проекта должна быть следующая структура:

djangogirls
├───manage.py
├───mysite
│        settings.py
│        urls.py
│        wsgi.py
│        __init__.py
└───requirements.txt

Открой файл в текстовом редакторе, который ты выбрала ранее.Давай внесём изменения в mysite/settings.py

Перейди к списку часовых поясов википедии и скопируй название своего часового пояса (GMT+6) (например, Asia/Bishkek).

В файле settings.py найди строку, содержащую TIME_ZONE, и измени её в соответствии со своим часовым поясом:

TIME_ZONE = 'Asia/Bishkek'

LANGUAGE_CODE = 'ru-ru'
Нам также необходимо добавить в настройки информацию о расположении статических файлов (мы познакомимся со статическими файлами и CSS в следующих главах). Спустись в конец файла и после переменной STATIC_URL добавь новую — STATIC_ROOT:

mysite/settings.py
STATIC_URL = '/static/'
STATIC_ROOT = BASE_DIR / 'static'
Когда наcтройка DEBUG имеет значение True, а настройка ALLOWED_HOSTS пуста, имя хост твоего веб-сайта сверяется со списком ['localhost', '127.0.0.1', '[::1]']. Ни одно из значений не будет соответствовать имени хоста на PythonAnywhere при публикации нашего приложения, поэтому нам необходимо изменить следующую настройку:

mysite/settings.py
ALLOWED_HOSTS = ['127.0.0.1', '.pythonanywhere.com']

Настройка базы данных

уществует множество различных баз данных, которые могут хранить данные для твоего сайта. Мы будем использовать стандартную — sqlite3.

Она уже выбрана по умолчанию в файле mysite/settings.py:

mysite/settings.py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
Чтобы создать базу данных для нашего блога, набери в командной строке следующее: python manage.py migrate (мы должны быть в директории djangogirls, где расположен файл manage.py). Если всё прошло успешно, то ты увидишь следующий результат:

command-line
(myvenv) ~/djangogirls$ python manage.py migrate
Operations to perform:
  Apply all migrations: auth, admin, contenttypes, sessions
Running migrations:
  Rendering model states... DONE
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying sessions.0001_initial... OK

  Запуск веб-сервера
Ты должна быть в директории, где расположен файл manage.py (в нашем случае — djangogirls). Запустим веб-сервер из командной строки: python manage.py runserver:


(myvenv) ~/djangogirls$ python manage.py runserver
Если ты работаешь в Windows, и команда падает с ошибкой UnicodeDecodeError, используй вместо неё другую:


(myvenv) ~/djangogirls$ python manage.py runserver 0:8000
Теперь тебе нужно проверить, работает ли веб-сайт — открой браузер (Firefox, Chrome, Safari, Internet Explorer или любой другой) и набери следующий адрес:


