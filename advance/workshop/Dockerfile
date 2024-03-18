FROM python:3.10-slim as builder

WORKDIR /app

COPY setup.py setup.py 
RUN pip install -e '.[dev]'

COPY talkshow talkshow
COPY settings.toml settings.toml
COPY .env .env
RUN flask adduser -u admin -p 1234
RUN flask addevent -n "Flask Conf" -d "2018-08-25"




FROM qnib/pytest as tester
WORKDIR /app
COPY --from=builder /app /app
COPY /tests /tests
#RUN py.test -v --cov-config .coveragerc --cov=talkshow -l --tb=short --maxfail=1 /tests/



FROM builder as final
CMD flask run
