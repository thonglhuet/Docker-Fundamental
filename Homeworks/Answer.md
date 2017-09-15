1.

1.
_qwer() {
   id= $(sudo docker ps -aq -f status=exited)
   sudo docker rm $(id)
}
alias kill_stop_container="_qwer"



_abcd(){
	docker stop $(docker ps -a -q)
}
alias stop_running_container="_abcd"



2.

.....


3.






Dockerfile


Sau khi build van phai mount requirement.
sudo docker run -v /media/framgiatw_flask_demo/:/home/framgiatw_flask_demo -ti thong:test3 /bin/bash
--------------------------------------------

FROM ubuntu:16.04

MAINTAINER 'luuhoangthong'

RUN DEBIAN_FRONTEND=noninteractive

RUN mkdir venv

RUN cd venv

RUN apt-get update
  apt-get install -y python python-dev python-pip python-virtualenv
RUN apt-get install libmysqlclient-dev
RUN pip install -r /home/framgiatw_flask_demo/requirements.txt
RUN pip install Flask-Migrate
RUN apt-get -y install mysql-server


RUN alembic current
RUN alembic revision -m "add department_employee_link"
RUN alembic upgrade head
RUN alembic current
RUN python seed.py
RUN gunicorn run:application -b :4000
-----------------------------------------------


4.


....