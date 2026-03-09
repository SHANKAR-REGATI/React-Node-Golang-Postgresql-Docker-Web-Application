# Pin a Specific base image version for stability
# Use debian for easier build utilities
# Use Separate stage for building the application
# Use Separate stage as base for development and production use cases to optimize for both scenarios
FROM golang:1.22-bullseye AS build-base

# Set a working directory
WORKDIR /app

# Copy only those files needed to install dependencies(better layer caching)
COPY go.mod go.sum ./

# Use cache mount to speed up install of existing dependencies
RUN --mount=type=cache,target=/go/pkg/mod \
    --mount=type=cache,target=/root/.cache/go-build \
    go mod download

# development stage
FROM build-base AS development

# install air for hot reload and delve for debugging
RUN go install github.com/cosmtrek/air@v1.43.0 && \
    go install github.com/go-delve/delve/cmd/dlv@v1.23.0

COPY . .

EXPOSE 8080

# run air so it watches for file changes and re-runs the application
CMD ["air", "-c", ".air.toml"]

# production stage
FROM build-base AS production

# Add non-root user for better security
RUN useradd -u 1001 nonroot

# Copy the rest of the application code
COPY . .

# Compile the code during build rather than during runtime
# Add Flags to statically link binary, so that binary can run anywhere
# without any system dependencies
# (especially in minimalistic distroless images like scratch)
RUN go build \
    -ldflags="-linkmode external -extldflags -static" \
    -tags netgo \
    -o golang-api

# Use Separate Stage for Deploying the Application
# Use Scratch distroless image as runtime doesn't need GO compiler
FROM scratch

# set the gin mode
ENV GIN_MODE=release

WORKDIR /app

# Copy user information from build stage (so nonroot user also exist here)
COPY --from=production /etc/passwd /etc/passwd
COPY --from=production /etc/group /etc/group

# switch to nonroot user
USER nonroot

# Copy the build artifact(compiled binary) from build stage
# Use --chown on copy commands to set permissions to non-root user
COPY --from=production --chown=nonroot:nonroot /app/golang-api golang-api

# expose the port on which application will run
EXPOSE 8080

CMD ["./golang-api"]