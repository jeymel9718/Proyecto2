FROM python:3

ENV FLASK_APP app.py

RUN pip install Flask

ADD app /home/app/

WORKDIR /home/app

EXPOSE 8000

CMD python -m flask run --port=8000 --host=0.0.0.0