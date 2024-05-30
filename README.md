# Project Manager Bot

![Project Manager Bot](https://koshka.top/uploads/posts/2021-11/1636536624_37-koshka-top-p-koshki-nezhnii-kotik-51.jpg)

## Описание

Project Manager Bot - это телеграм-бот, предназначенный для управления проектами. Бот позволяет добавлять новые проекты, обновлять информацию о них, привязывать навыки к проектам, а также удалять проекты. Все данные хранятся в базе данных SQLite.

## Функционал

- **Добавление нового проекта**: команда `/new_project`
- **Просмотр всех проектов**: команда `/projects`
- **Обновление информации о проекте**: команда `/update_projects`
- **Привязка навыков к проекту**: команда `/skills`
- **Удаление проекта**: команда `/delete`
- **Информация о командах**: команда `/info`

## Установка

1. Склонируйте репозиторий:
    ```bash
    git clone https://github.com/yernur0/project-manager-bot.git
    ```

2. Установите необходимые зависимости:
    ```bash
    pip install -r requirements.txt
    ```

3. Создайте базу данных SQLite и необходимые таблицы:
    ```sql
    CREATE TABLE users (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        telegram_id INTEGER NOT NULL UNIQUE,
        username TEXT
    );

    CREATE TABLE projects (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        user_id INTEGER,
        project_name TEXT,
        description TEXT,
        link TEXT,
        status_id INTEGER,
        FOREIGN KEY (user_id) REFERENCES users (id),
        FOREIGN KEY (status_id) REFERENCES statuses (id)
    );

    CREATE TABLE statuses (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        status_name TEXT
    );

    CREATE TABLE skills (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        skill_name TEXT
    );

    CREATE TABLE project_skills (
        project_id INTEGER,
        skill_id INTEGER,
        FOREIGN KEY (project_id) REFERENCES projects (id),
        FOREIGN KEY (skill_id) REFERENCES skills (id)
    );
    ```

4. Настройте переменные окружения (например, `config.py`):
    ```python
    TOKEN = 'your_telegram_bot_token'
    DATABASE = 'path_to_your_database.db'
    ```

## Использование

Запустите бота:
```bash
python main.py
