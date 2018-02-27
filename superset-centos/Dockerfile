FROM centos:latest

LABEL maintainer="Sateesh Kota <sateekumar.529@gmail.com>" \
	name="Superset image"
LABEL Description="Superset is an open source platform for analytics and business intelligence."
#Superset Version
ARG SUPERSET_VERSION=0.22.1


RUN yum upgrade python-setuptools && \
	yum install -y epel-release && \
	yum install -y gcc gcc-c++ libffi-devel python-devel python-pip python-wheel openssl-devel libsasl2-devel openldap-devel && \
	pip install --upgrade setuptools pip && \
	pip install superset==${SUPERSET_VERSION}
RUN printf "admin\nadmin\nroot\nroot@localhost\nadmin\nadmin\n" | fabmanager create-admin --app superset && \
	superset db upgrade && \
	superset load_examples && \
	superset init

EXPOSE 8088
HEALTHCHECK CMD ["curl", "-f", "http://localhost:8088/health"]
ENTRYPOINT ["superset"]
CMD ["runserver"]