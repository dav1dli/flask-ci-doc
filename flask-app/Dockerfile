FROM openshift/python
ADD . .
RUN pip install -r requirements.txt
EXPOSE 8080
CMD python run.py
