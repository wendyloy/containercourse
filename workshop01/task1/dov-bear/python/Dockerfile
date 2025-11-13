FROM python:3.13

WORKDIR /app

COPY public public
COPY templates templates
COPY requirements.txt .
COPY *.py .
COPY run.sh .

RUN pip install -r requirements.txt

ENV PORT=5000 INSTANCE_NAME="" INSTANCE_HASH=""

EXPOSE ${PORT}

ENTRYPOINT python main.py
# CMD [ "--port", "3000", "--name", "", "--hash", ""]
