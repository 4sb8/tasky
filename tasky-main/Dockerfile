# Building the binary of the App
FROM golang:1.19 AS build

WORKDIR /go/src/tasky
COPY . .
RUN go mod download
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o /go/src/tasky/tasky


FROM alpine:3.17.0 as release

# Inject developer name into wizexercise.txt
# Passed via --build-arg DEVELOPER_NAME at build time by CI/CD pipeline
ARG DEVELOPER_NAME
RUN echo "$DEVELOPER_NAME" > /wizexercise.txt

WORKDIR /app
COPY --from=build  /go/src/tasky/tasky .
COPY --from=build  /go/src/tasky/assets ./assets
EXPOSE 8080
ENTRYPOINT ["/app/tasky"]


