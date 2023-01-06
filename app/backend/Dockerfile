
FROM python:3.9

COPY . .

ENV SECRET_KEY 1234
# run pip upgrade
RUN pip install -U ipdb
RUN pip install psycopg
RUN pip install psycopg2-binary
RUN pip install -r requirements.txt  

# port where the Django app runs  
EXPOSE 8000  
# start server  
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]