FROM 172.30.1.1:5000/openshift/python
ADD . .
RUN pip install -r requirements.txt
EXPOSE 8080
CMD python run.py
