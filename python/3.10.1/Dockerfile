FROM python:3.10.1

RUN apt-get update && \
    apt-get install -y tesseract-ocr libtesseract-dev && \
    pip3 install pillow pytesseract APScheduler werkzeug Flask requests click gunicorn lxml redis

WORKDIR /app

EXPOSE 8010:8010

CMD ["top", "-b"]

