#FROM python:3.9.23-alpine3.22
FROM python:3.9-slim
EXPOSE 8080
WORKDIR /opt/server
COPY requirements.txt .
COPY payment.ini .
COPY *.py .
RUN addgroup --system roboshop && adduser --system --ingroup roboshop roboshop \
    && chown -R roboshop:roboshop /opt/server \
    && pip3 install -r requirements.txt
USER roboshop
CMD ["uwsgi", "--ini", "payment.ini"]
#CMD ["sleep", "1000"]
# FROM python:3.9
# EXPOSE 8080
# WORKDIR /opt/server
# COPY requirements.txt .
# COPY *.py .
# COPY payment.ini .
# RUN pip3 install -r requirements.txt
# CMD ["uwsgi", "--ini", "payment.ini"]