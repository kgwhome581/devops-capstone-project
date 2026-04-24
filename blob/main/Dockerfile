# Используем официальный базовый образ Python
FROM python:3.9-slim

# Установка рабочей директории в контейнере
WORKDIR /app

# Копирование требований и их установка (кэшируемый слой)
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Копирование ВСЕХ файлов приложения в текущую директорию контейнера
# Это критически важно, чтобы COPY . . включало все подпапки (service, и др.)
COPY . .

# Создание пользователя с ограниченными правами для безопасности (non-root)
# Мы даем ему права на владение папкой /app перед переключением
RUN useradd -m theuser && chown -R theuser:theuser /app
USER theuser

# Открытие порта 8080 для Flask/Gunicorn
EXPOSE 8080

# Запуск приложения через Gunicorn
CMD ["gunicorn", "--bind", "0.0.0.0:8080", "service:app"]
