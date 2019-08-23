FROM docker.io/centos/python-36-centos7
ADD . .
RUN pip install -r requirements.txt
EXPOSE 8080
CMD python run.py
