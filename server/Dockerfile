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

ENV DJANGO_PORT=8000 \
    DJANGO_HOST=localhost \
    ENVIROMENT=development \
    CORS_ALLOWED_ORIGINS=http://87.236.23.222,http:astrotech-appspace.space, \
    PROJECT_DIR=/app \
    DJANGO_SECRET_KEY=python3manage.pyrunserver

RUN python3 manage.py collectstatic --no-input

RUN chmod 700 -R scripts

EXPOSE ${DJANGO_PORT}

CMD ["./scripts/start_api.sh"]