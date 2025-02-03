FROM rabbitmq:3.12-management

COPY rabbitmq.conf /etc/rabbitmq
COPY definitions.json /etc/rabbitmq/definitions.json

ENV RABBITMQ_SERVER_ADDITIONAL_ERL_ARGS="-rabbitmq_management load_definitions \"/etc/rabbitmq/definitions.json\""

RUN cat /etc/rabbitmq/rabbitmq.conf