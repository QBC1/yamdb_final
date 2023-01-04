FROM python:3.7-slim

WORKDIR /app

COPY requirements.txt /app

RUN python -m pip install --upgrade pip

RUN pip install -r requirements.txt --no-cache-dir  

COPY . /app

CMD ["gunicorn", "api_yamdb.wsgi:application", "--bind", "0:5000" ]
