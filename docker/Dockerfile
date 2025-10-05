FROM python:3.9-slim

WORKDIR /app

COPY . .

RUN pip install --no-cache-dir -r requirements.txt

ENV AWS_ACCESS_KEY_ID = my_access_key_id
ENV AWS_SECRET_ACCESS_KEY = my_secret_access_key

EXPOSE 5001

CMD ["python", "main.py"]