FROM python:3.14.0a3-slim-bullseye
WORKDIR /app
COPY requirements.txt /app/
COPY dev /app/

RUN python -m pip install --no-cache-dir -r requirements.txt


COPY . .

EXPOSE 8000

ENTRYPOINT [ "python3" ]
CMD [ "manage.py","runserver","0.0.0.0:8000" ]
