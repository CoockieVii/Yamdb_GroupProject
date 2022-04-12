
# Проект YaMDb :computer:
Описание проекта
----------
Проект **YaMDb** собирает **отзывы (Review)** пользователей на **произведения (Title)** Произведения делятся на категории: "Книги", "Фильмы", "Музыка". Список **категорий (Category)** может быть расширен.
Сами произведения в **YaMDb** не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
В каждой категории есть **произведения**: книги, фильмы или музыка. Например, в категории "Книги" могут быть произведения "Винни Пух и все-все-все" и "Марсианские хроники", а в категории "Музыка" — песня "Давеча" группы "Насекомые" и вторая сюита Баха. Произведению может быть присвоен жанр из списка предустановленных (например, "Сказка", "Рок" или "Артхаус"). Новые жанры может создавать только администратор.
Благодарные или возмущённые пользователи оставляют к произведениям текстовые **отзывы (Review)** и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — **рейтинг** (целое число). На одно произведение пользователь может оставить только один отзыв.

----------
# Алгоритм регистрации пользователей
* Пользователь отправляет POST-запрос с параметром email на `/api/v1/auth/email/`.
* YaMDB отправляет письмо с кодом подтверждения (confirmation_code) на адрес email.
* Пользователь отправляет POST-запрос с параметрами email и confirmation_code на `/api/v1/auth/token/`, в ответе на запрос ему приходит token (JWT-токен).
* Если письмо не дошло по какой то причине или был утерян token пользователь может выполнить вышеуказанные действия повторно.
----------
# Пользовательские роли

**Аноним** — может просматривать описания произведений, читать отзывы и комментарии.

**Аутентифицированный пользователь (user)** — может, как и Аноним, читать всё, дополнительно он может публиковать отзывы и ставить оценку произведениям (фильмам/книгам/песенкам), может комментировать чужие отзывы; может редактировать и удалять свои отзывы и комментарии. Эта роль присваивается по умолчанию каждому новому пользователю.

**Модератор (moderator)** — те же права, что и у Аутентифицированного пользователя плюс право удалять любые отзывы и комментарии.

**Администратор (admin)** — полные права на управление проектом и всем его содержимым. Может создавать и удалять произведения, категории и жанры. Может назначать роли пользователям.

**Администратор Django** — полные права на управление всем контентом проекта. Может создавать и удалять произведения, категории и жанры, имеет доступ к административному интерфейсу Django, может назначать роли пользователям, устанавливать их права.

**Суперюзер Django** — те же права, что и у администратора Django, не зависимо от установленной роли.

----------
# Установка
Системные требования
----------
* Python 3.9+
* Works on Linux, Windows, macOS, BSD

Стек технологий
----------
* Python 3.9
* Django 2.2
* Django Rest Framework
* Pytest
* Simple-JWT
* SQLite3

Установка проекта из репозитория (Windows)
----------
1. Клонировать репозиторий и перейти в него в командной строке:
```bash
git clone 'git@github.com:valeriy-kirichenko/api_yamdb.git'
или
git clone 'git@github.com:CoockieVii/api_yamdb.git'

cd api_yamdb
```
2. Cоздать и активировать виртуальное окружение:
```bash
python -m venv venv

source venv/Scripts/activate
```
3. Установить зависимости из файла ```requirements.txt```:
```bash
python -m pip install --upgrade pip

pip install -r requirements.txt
```
4. Выполнить миграции:
```bash
cd api_yamdb

python manage.py migrate
```
5. Загрузить данные в БД:
```bash
cd api_yamdb/api_yamdb

python manage.py importcsv
```
6. Запустить проект (в режиме сервера Django):
```bash
python manage.py runserver
```
----------
Авторы:
----------
* **Кириченко Валерий Михайлович**
GitHub - [valeriy-kirichenko](https://github.com/valeriy-kirichenko)
* **Валитов Ильмир Илсурович**
GitHub - [CoockieVii](https://github.com/CoockieVii)
----------
Документация к проекту с примерами запросов и ответов
----------
Документация для API [доступна по ссылке](http://localhost:8000/redoc/) после установки приложения.