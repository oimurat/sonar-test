FROM python:3.12

ENV PYTHONUNBUFFERED=1 \
    PIP_NO_CACHE_DIR=1 \
    PIP_DISABLE_PIP_VERSION_CHECK=1

WORKDIR /app

COPY fastapi/requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

RUN python fastapi/api/test.py