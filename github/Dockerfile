FROM golang:1.19-alpine AS build-stage

WORKDIR /app

COPY go.mod .
RUN go mod download

COPY *.go .
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o /repo-1

FROM alpine AS build-release-stage

WORKDIR /app

COPY --from=build-stage /repo-1 /repo-1

EXPOSE 80

ENTRYPOINT ["/repo-1"]
