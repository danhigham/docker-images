FROM python:alpine

RUN apk add git
RUN pip install --upgrade google-api-python-client google-auth-httplib2 google-auth-oauthlib

RUN git clone https://github.com/danhigham/gmail-purge.git
CMD ["./gmail-purge/purge.py"]
