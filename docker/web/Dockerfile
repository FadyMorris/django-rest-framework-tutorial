#FROM ubuntu:18.04
FROM ubuntu:24.04
RUN apt-get update
RUN apt-get install -y apt-utils vim curl apache2 apache2-utils tree
RUN apt-get -y install python3 python3-venv libapache2-mod-wsgi-py3
RUN ln /usr/bin/python3 /usr/bin/python
RUN python -m venv /root/env
ENV PATH="/root/env/bin:$PATH"
##RUN ln /usr/bin/pip3 /usr/bin/pip
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
# pip install commands
WORKDIR /var/www/
ADD ./config/demo_site.conf /etc/apache2/sites-available/demo_site.conf
EXPOSE 8000
RUN pip install --upgrade pip
# RUN pip install djangorestframework Django psycopg[binary] ptvsd ipython django-debug-toolbar
COPY ./config/requirements.txt /tmp
RUN pip install -r /tmp/requirements.txt
RUN a2ensite demo_site.conf
RUN a2enmod proxy
RUN a2enmod proxy_http
RUN a2enmod proxy_balancer
RUN a2enmod lbmethod_byrequests
RUN service apache2 start
#RUN service apache2 reload
#EXPOSE 80 3500
CMD ["apache2ctl", "-D", "FOREGROUND"]
#CMD ["tail", "-f", "/dev/null"]

