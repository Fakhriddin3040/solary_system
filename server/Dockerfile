FROM python:3.12-alpine

# Устанавливаем зависимости
RUN apk --no-cache add gcc musl-dev libffi-dev openssl-dev

# Устанавливаем рабочую директорию
WORKDIR ${PROJECT_DIR}

# Копируем requirements.txt и устанавливаем зависимости
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

COPY .env.example .env

RUN python3 manage.py collectstatic --no-input

RUN chmod 700 -R scripts

EXPOSE ${DJANGO_PORT}

CMD ["./scripts/start_api.sh"]