# multi-stage build for compiled languages and the source code is not exposed and reduce image size
# build stage
# second stage only has the binary and public and templates folder to run

FROM golang:1.25-bookworm AS builder

WORKDIR /src

COPY go.* .
COPY main.go .

RUN go get && go build -o main main.go

FROM debian:bookworm

WORKDIR /app

#install curl
RUN apt update && apt install -y curl

COPY --from-builder /src/main .
COPY public public
COPY templates templates

ENV PORT=5000 INSTANCE_NAME="dov-bear"

# wait 15s before start, freq 30s, and retry 3 times. fastest time to detect error is 1.5mins
HEALTHCHECK --interval=30s --timeout=3s --start_period=15s --retries=3 \
    CMD curl losthost:${PORT}/health || exit 1

EXPOSE ${PORT}

ENTRYPOINT /app/main