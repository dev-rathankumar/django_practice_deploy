# Purpose: A Dockerfile is a step-by-step instruction file that tells Docker how to build and run our application.
FROM python:3.10-slim

ENV PYTHONUNBUFFERED=1
ENV PYTHONDONTWRITEBYTECODE=1

WORKDIR /app

RUN apt-get update && apt-get install -y --no-install-recommends \
    gcc \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8000

# gunicorn = production/application server, clickmart_main.wsgi:application = Django entry point, --bind 0.0.0.0:8000 = external traffic. Reminaing: tuning options
# A worker is just one instance of your Django app running inside Gunicorn.
CMD ["gunicorn", "clickmart_main.wsgi:application", "--bind", "0.0.0.0:8000", "--workers", "3" , "--timeout", "180"]