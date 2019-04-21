FROM python:2.7.16-jessie
#Setting PYTHONUNBUFFERED=TRUE or PYTHONUNBUFFERED=1 (they are equivalent) allows for log messages to be immediately dumped to the stream instead of being buffered. This is useful for receiving timely log messages and avoiding situations where the application crashes without emitting a relevant message due to the message being "stuck" in a buffer.
ENV PYTHONUNBUFFERED 1

#Installing required packages which not present in image 
RUN apt-get update && apt-get -y install git libpq-dev python-dev postgresql-client-common 
RUN mkdir -p /usr/share/man/man1 && mkdir -p /usr/share/man/man7 && apt-get install -y --no-install-recommends postgresql-client 

#Cloning app from repo, changing psycopg2 version. because 2.6.1 is broken/outdated: https://github.com/psycopg/psycopg2/issues/594 , https://jamaicandevelopers.com/Members/oshane--bailey/error-could-not-determine-postgresql-version-from-10.0 . Installing requirements
RUN git clone git://github.com/kirpit/django-sample-app.git django && cd django && sed -i 's/2.6.1/2.7.3.1/' requirements.txt && pip install -r requirements.txt && pip install uwsgi
WORKDIR /django/projectname
#Fixing wsgi.py to be executed by uwsgi
RUN sed -i 's/{{ project_name }}/projectname/g' /django/projectname/wsgi.py  &&  awk 'NR==17{$0="import sys\nBASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))\nsys.path.append(BASE_DIR)\n"$0}1' /django/projectname/wsgi.py > /django/projectname/wsgi.py__ && mv /django/projectname/wsgi.py__ /django/projectname/wsgi.py  
#Copy decrypted creds/settings 
COPY default.py /django/projectname/settings/
COPY local.py /django/projectname/settings/
#Run migrate and  uwsgi
RUN cd /django/projectname/ && ./manage.py migrate 
CMD uwsgi --http :80 --wsgi-file wsgi.py --static-map /static=/django/static --master --pidfile=/tmp/project-master.pid

