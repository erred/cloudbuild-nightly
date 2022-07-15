FROM golang:alpine AS build
ENV GOMEMLIMIT=3758096384 \
    GOGC=off
RUN apk add --no-cache bash gcc git musl-dev && \
    go install golang.org/dl/gotip@latest && \
    gotip download && \
    rm -rf /root/sdk/gotip/pkg/linux_* && \
    GOBIN=/root/sdk/gotip/bin gotip install honnef.co/go/tools/cmd/staticcheck@latest && \
    GOBIN=/root/sdk/gotip/bin gotip install github.com/google/ko@latest

FROM alpine
ENV PATH=/root/sdk/gotip/bin:/root/go/bin:$PATH \
    GOMEMLIMIT=3758096384 \
    GOGC=off
COPY --from=build /root/sdk/gotip /root/sdk/gotip
WORKDIR /workspace
ENTRYPOINT [ "go" ]
