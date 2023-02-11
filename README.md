# Infra_sp2
____
![Workflow](https://github.com/QBC1/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)
### Сайт расположен на домене:
#### https://qbci.sytes.net/

### Документация к сайту:
#### https://qbci.sytes.net/redoc/
____
## Описание
Проект infra собирает отзывы (Review) пользователей на произведения (Titles). Произведения делятся на категории: «Книги», «Фильмы», «Музыка». Список категорий (Category) может быть расширен администратором. Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку. В каждой категории есть произведения: книги, фильмы или музыка. Например, в категории «Книги» могут быть произведения «Винни-Пух и все-все-все» и «Марсианские хроники», а в категории «Музыка» — песня «Давеча» группы «Насекомые» и вторая сюита Баха. Произведению может быть присвоен жанр (Genre) из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»). Новые жанры может создавать только администратор. Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы (Review) и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — рейтинг (целое число). На одно произведение пользователь может оставить только один отзыв.
____
### Как запустить проект:
```
git clone https://github.com/QBC1/infra_sp2.git
cd infra_sp2
cd api_yamdb    
```
Создаем и активируем виртуальное окружение:
```
python3 -m venv venv
source /venv/bin/activate (source /venv/Scripts/activate - для Windows)
python -m pip install --upgrade pip
```
Ставим зависимости из requirements.txt:
```
pip install -r requirements.txt
```
Переходим в папку с файлом docker-compose.yaml:
```
cd infra
```
Поднимаем контейнеры (infra_db_1, infra_web_1, infra_nginx_1):
```
sudo docker-compose up -d --build
```
Выполняем миграции:
```
sudo docker-compose exec web python manage.py migrate
```
Создаем суперпользователя:
```
sudo docker-compose exec web python manage.py createsuperuser
```
Собираем статику:
```
sudo docker-compose exec web python manage.py collectstatic --no-input
```
Создаем дамп базы данных:
```
sudo docker-compose exec web python manage.py dumpdata > fixtures.json
```
Команда для импорта (восстановления) с loaddata:
```
sudo docker-compose exec web python manage.py loaddata fixtures.json
```
Останавливаем контейнеры:
```
sudo docker-compose down -v
```
Шаблон наполнения .env расположенный по пути infra/.env:
```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
```
____
Данный проект реализовал данный [человек](https://github.com/QBC1)
