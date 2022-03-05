# ./Dockerfile

FROM golang:1.16-alpine AS builder

# Move to working directory (/build).
# WORKDIR /build

# Copy and download dependency using go mod.
# COPY go.mod go.sum ./
# RUN go mod download

# Copy the code into the container.
# COPY . .

# Set necessary environment variables needed for our image 
# and build the API server.
# ENV CGO_ENABLED=0 GOOS=linux GOARCH=amd64
# RUN go build -ldflags="-s -w" -o apiserver .

# FROM scratch

# Copy binary and config files from /build 
# to root folder of scratch container.
# COPY --from=builder ["/build/apiserver", "/build/.env", "/"]

# Export necessary port.
# EXPOSE 80

# Command to run when starting the container.
# ENTRYPOINT ["/apiserver"]


# CMD ["/dist/main"]


# FROM golang:alpine

# Set necessary environmet variables needed for our image
ENV GO111MODULE=on \
    CGO_ENABLED=0 \
    GOOS=linux \
    GOARCH=amd64

# Move to working directory /build
WORKDIR /build

# Copy and download dependency using go mod
COPY go.mod .
COPY go.sum .
RUN go mod download

# Copy the code into the container
COPY . .

# Build the application
# RUN go build -o main .
RUN go build -ldflags="-s -w" -o main .

# Move to /dist directory as the place for resulting binary folder
WORKDIR /dist

# Copy binary from build to main folder
RUN cp /build/main .

# Export necessary port
EXPOSE 80

# Command to run when starting the container
CMD ["/dist/main"]