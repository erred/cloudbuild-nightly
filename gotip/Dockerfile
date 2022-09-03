FROM golang:alpine AS build
ENV CGO_ENABLED=0
RUN apk add --no-cache bash gcc git musl-dev && \
    go install golang.org/dl/gotip@latest && \
    gotip download && \
    rm -rf /root/sdk/gotip/pkg/linux_* && \
    GOBIN=/root/sdk/gotip/bin gotip install honnef.co/go/tools/cmd/staticcheck@latest && \
    GOBIN=/root/sdk/gotip/bin gotip install github.com/google/ko@latest

FROM alpine
ENV CGO_ENABLED=0
ENV PATH=/root/sdk/gotip/bin:/root/go/bin:$PATH
COPY --from=build /root/sdk/gotip /root/sdk/gotip
WORKDIR /workspace
ENTRYPOINT [ "go" ]
