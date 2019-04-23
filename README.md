# Mercuryo.io
Тестовое задание на должность PHP/Go разработчика.

# Описание

В данном проекте, вам нужно будет создать сайт с обзорами на различные книги. Пользователи смогут регистрироваться на вашем сайте, а также авторизовываться, используя свои учетные данные (логин и пароль). После авторизации, они должны иметь возможность искать книги, оставлять о них отзывы и видеть отзывы других пользователей. Вы также воспользуетесь сторонним API, предоставляемый сайтом Goodreads (тоже сайт книжных отзывов), таким образом получая доступ к рейтингам более обширной аудитории, которые вам нужно будет задействовать в своем проекте. И наконец, пользователи смогут программным путем запрашивать подробную информацию о книгах и об их отзывах, пользуясь вашим веб-сайтовским API.

# Goodreads API

Goodreads - это популярный сайт, посвященный книжным отзывам. В данном проекте мы воспользуемся их API, чтобы получить доступ к отзывам каждой отдельной книги.

Перейдите на https://www.goodreads.com/api и зарегистрируйте Goodreads аккаунт, конечно, если у вас еще нет данной учетной записи.
Перейдите по ссылке https://www.goodreads.com/api/keys и подайте заявку на получение ключа API. Поля "Application name" (название приложения) и "Company name" (название компании) можете просто заполнить текстом "project1", и нет необходимости включать ссылку приложения, callback URL или ссылку поддержки/запасную/дополнительную (support URL).
Далее вы должны увидеть свой ключ API (В данной проекте, нас интересует только "key" (ключ), не "secret".)
Теперь вы можете применить этот ключ API для создания запросов, направленных на Goodreads API. [Здесь](https://www.goodreads.com/api/index) вся необходимая документация. 

# Требования
Хорошо, теперь пришло время перейти к непосредственному созданию вашего веб-приложения! Вот требования:
Сайт должен быть написан на YII2 или другом PHP фреймворке, за исключением импортирования, которое должно быть на писано на Go lang.

* **Регистрация**: Пользователи должны иметь возможность регистрироваться на вашем сайте, как минимум ваш сайт должен требовать никнейм (username) и пароль (password).
* **Авторизация**: Зарегистрировавшиеся пользователи должны иметь возможность авторизовываться с помощью своих учетных данных (логина и пароля).
* **Разлогинивание**: Авторизованные пользователи должны иметь возможность разлогиниваться с сайта.
* **Импортирование**: К данному проекту прилагается файл под названием books.csv, который представляет из себя таблицу формата CSV, содержащую данные 5000 различных книг. У каждой книги есть номер ISBN, название (title), автор (author) и дата публикации (publication date). В Go файле под названием `import.go`, отдельно от вашего веб-приложения, напишите программу, которая будет брать информацию о книгах и заносить ее в базу данных MySQL. Вам сперва нужно будет решить, какие таблицы(цу) вы будете создавать, какие столбики должны быть у данных таблиц и как они должны взаимодействовать друг с другом. Запустите вашу программу командой `go run import.go`, таким образом вы импортируете данные о книгах в вашу базу. Отправляя проект на проверку, не забудьте включить данную программу в свой код и схему БД.
* **Поиск**: Как только пользователь авторизуется, он должен быть перенаправлен на страницу, где он сможет осуществлять поиск интересующей его книги. У пользователей должна быть возможность вводить книжный ISBN номер, название книги или имя автора книги. После произведения сайтом операции поиска, он должен отобразить список возможных результатов или отобразить сообщение, при отсутствии каких-либо результатов. Если пользователь введет только часть названия книги, неполный номер ISBN или неполное имя автора, ваша страница должна и под них выдать результаты!
* **Страница Описания Книги**: Когда пользователи нажмут на книгу, предоставленной страницей поиска, они должный быть перенаправлены на страницу книги, с подробной детализацией рассматриваемой работы: ее название, автор, дата публикации, номер ISBN и какие-либо отзывы, оставленные пользователями на вашем сайте.
* **Оставление Отзыва Review Submission**: Находясь на странице с описанием книги, у пользователя должна быть возможность оставлять отзывы, в которые будет входить оценка по шкале от 1 до 5 баллов, а также текст, где пользователь сможет записывать свое мнение о книге. Пользователю нельзя публиковать несколько отзывов на одну и ту жу книгу.
* **Отзывы Goodreads**: На странице книги также должны быть показаны (если есть) средняя оценка и количество оценок, полученных книгой от ресурса Goodreads.
* **Доступ к API**: Если пользователь пошлет GET-запрос на ваш веб-страничный маршрут /api/<isbn>, где <isbn> является номером ISBN, тогда ваш веб-сайт должен вернуть JSON-объект, содержащий название книги (title), автора (author), дату публикации (year), номер ISBN, количество отзывов (review count) и среднюю оценку (average score). В результате должен получиться JSON-объект следующего формата:
```json
{
    "title": "Mastering Bitcoin: Programming the Open Blockchain",
    "author": "Andreas M. Antonopoulos",
    "year": 2017,
    "isbn": "9781491954386",
    "review_count": 28,
    "average_score": 5.0
}
```
Если запрашиваемого номера ISBN нет в вашей базе данных, то ваш сайт должен вернуть ошибку 404.

Вы должны использовать только "чистые" (raw) SQL-команды.

Файл README.md содержит короткое описание вашего проекта: что содержится в каждом файле и (по желанию) какая-либо еще дополнительная информация, которую нам стоило бы знать при проверке вашего проекта.

Помимо этих требований, вы можете добавить в проект свои идеи. Дизайн, вид и общее ощущение от использования сайта могут быть свободно дополнены вашим собственным видением!

**Проект должен включать в себя все необходимое для разворачивания сервиса в Docker-контейнере.**

**После выполнения проекта необходимо сделать pull request в этот репозиторий.**
