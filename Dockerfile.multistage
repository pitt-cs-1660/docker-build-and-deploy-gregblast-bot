# =============================================================================
# stage 1: builder
# =============================================================================
# Set base image
FROM golang:1.23 AS builder

# Set working directory
WORKDIR /app

# Copy all files needed for build into the working directory
COPY go.mod main.go .
COPY templates/ ./templates

# Compile the application into a static binary and put into the working directory
RUN CGO_ENABLED=0 go build -o BandNames .

# =============================================================================
# stage 2: runtime (final image)
# =============================================================================
# Set base image
FROM scratch

# Set working directory
WORKDIR /app

# Copy the compiled binary and templates from builder
COPY --from=builder ./BandNames .
COPY --from=builder ./templates ./templates

# Command to run the binaries
CMD ["/BandNames"]