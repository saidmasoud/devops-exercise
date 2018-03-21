FROM python:3.7-rc-alpine

ARG MONGODB

WORKDIR /usr/src/app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY . /usr/src/app

CMD ["python","api.py"]
