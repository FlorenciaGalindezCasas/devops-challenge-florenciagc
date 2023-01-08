#  especifica la imagen principal a partir de la cual está construyendo
FROM python:3.9

# copia todas las carpetas
COPY . .

ENV SECRET_KEY 1234

# run pip upgrade
RUN pip install -U ipdb
RUN pip install psycopg
RUN pip install psycopg2-binary
RUN pip install -r requirements.txt  

# puerto donde corre la app Django  
EXPOSE 8000  

# start server  
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]