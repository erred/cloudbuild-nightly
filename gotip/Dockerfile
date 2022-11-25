FROM golang:alpine AS build
ENV CGO_ENABLED=0 \
    GOFLAGS=-trimpath
RUN apk add --no-cache bash curl gcc git musl-dev && \
    go install golang.org/dl/gotip@latest && \
    gotip download && \
    rm -rf /root/sdk/gotip/pkg/linux_* && \
    curl -Lo /usr/local/bin/skaffold https://storage.googleapis.com/skaffold/builds/latest/skaffold-linux-amd64 && \
    chmod +x /usr/local/bin/skaffold

FROM alpine
RUN apk add --no-cache git
ENV CGO_ENABLED=0 \
    GOFLAGS=-trimpath
ENV PATH=/root/sdk/gotip/bin:/root/go/bin:$PATH
COPY --from=build /usr/local/bin/skaffold /usr/local/bin/skaffold
COPY --from=build /root/sdk/gotip /root/sdk/gotip
WORKDIR /workspace
ENTRYPOINT [ "go" ]
