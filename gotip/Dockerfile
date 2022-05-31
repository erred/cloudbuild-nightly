FROM golang:alpine AS build
RUN apk add --no-cache bash gcc git musl-dev && \
    go install golang.org/dl/gotip@latest && \
    gotip download && \
    GOBIN=/root/sdk/gotip/bin gotip install honnef.co/go/tools/cmd/staticcheck@latest

FROM alpine
ENV PATH=/root/sdk/gotip/bin:/root/go/bin:$PATH
COPY --from=build /root/sdk/gotip /root/sdk/gotip
WORKDIR /workspace
ENTRYPOINT [ "go" ]
