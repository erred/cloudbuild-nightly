FROM golang:alpine AS build
ENV CGO_ENABLED=0 \
    GOFLAGS=-trimpath
RUN apk add --no-cache bash gcc git musl-dev && \
    go install golang.org/dl/gotip@latest && \
    gotip download && \
    rm -rf /root/sdk/gotip/pkg/linux_* && \
    GOBIN=/root/sdk/gotip/bin gotip install -ldflags='-s -w' github.com/google/ko@latest

# GOBIN=/root/sdk/gotip/bin go install -ldflags='-s -w' honnef.co/go/tools/cmd/staticcheck@latest && \

FROM alpine
RUN apk add --no-cache git
ENV CGO_ENABLED=0 \
    GOFLAGS=-trimpath
ENV PATH=/root/sdk/gotip/bin:/root/go/bin:$PATH
COPY --from=build /root/sdk/gotip /root/sdk/gotip
WORKDIR /workspace
ENTRYPOINT [ "go" ]
