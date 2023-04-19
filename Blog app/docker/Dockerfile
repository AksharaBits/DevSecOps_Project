FROM python:3.9.4-alpine

EXPOSE 8000

ENV WORKING_DIR /app

# Python dependencies
COPY requirements.txt .
# update docker-iamage packages
 
# update pip 
RUN pip install --upgrade pip
# install psycopg for connect to pgsql
RUN pip install psycopg2-binary
RUN pip3 install --no-cache-dir -r requirements.txt

WORKDIR $WORKING_DIR

# Project files
COPY manage.py $WORKING_DIR/manage.py
COPY blog $WORKING_DIR/blog
COPY mysite $WORKING_DIR/mysite

# Run migrations, and load the database with fixtures
RUN python manage.py migrate && python manage.py loaddata users posts comments
#RUN python manage.py test blog --verbosity=2

ENTRYPOINT ["python", "manage.py"]
CMD ["runserver", "0.0.0.0:8000"]
