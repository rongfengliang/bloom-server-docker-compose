FROM buildpack-deps:stretch-curl
WORKDIR /app
RUN wget https://github.com/valeriansaliou/bloom/releases/download/1.25/v1.25-amd64.tar.gz \
    && tar zxvf v1.25-amd64.tar.gz \
    && rm -rf v1.25-amd64.tar.gz && chmod +x /app/bloom/bloom
CMD [ "/app/bloom/bloom","-c","/app/bloom/config.cfg" ]