FROM alpine:latest AS builder

WORKDIR /app
COPY ./backend-services/prometheus-grafana-stack/go/hello-world-service .

RUN /bin/sh -c "apk add --no-cache go && \
                go mod tidy && \
                go build -o main ."

FROM alpine:latest
WORKDIR /app
COPY --from=builder /app/main .
EXPOSE 80
ENTRYPOINT ["./main"]

# Building the docker image from `cd ../../../../`: docker build -t go-hello-world-service:0.1.0 -f ./backend-services/prometheus-grafana-stack/go/hello-world-service/Dockerfile .
# Run the docker container: docker run --rm -p 5002:80 -d go-hello-world-service:0.1.0 