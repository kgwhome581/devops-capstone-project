# Использование официального образа Python
FROM python:3.9-slim

# Установка рабочей директории
WORKDIR /app

# Копирование файлов зависимостей и их установка
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Копирование исходного кода приложения
COPY service/ ./service/

# Создание пользователя с ограниченными правами для безопасности
RUN useradd -m appuser && chown -R appuser:appuser /app
USER appuser

# Открытие порта приложения
EXPOSE 8080

# Команда для запуска приложения через Gunicorn
CMD ["gunicorn", "--bind", "0.0.0.0:8080", "service:app"]
