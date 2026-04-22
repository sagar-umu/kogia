ARG DEBIAN_VERSION=trixie-slim
FROM debian:${DEBIAN_VERSION} AS build-sortmerna
ARG SORTMERNA_VERSION=4.4.0
WORKDIR /build
RUN apt-get update && apt-get install -y --no-install-recommends \
        curl ca-certificates bash binutils \
    && rm -rf /var/lib/apt/lists/*
RUN curl -O -L https://github.com/biocore/sortmerna/releases/download/v${SORTMERNA_VERSION}/sortmerna-${SORTMERNA_VERSION}-Linux.sh
RUN bash sortmerna-${SORTMERNA_VERSION}-Linux.sh --skip-license
RUN strip /build/bin/sortmerna

FROM debian:${DEBIAN_VERSION}
ARG SORTMERNA_VERSION=4.4.0
WORKDIR /
COPY --from=build-sortmerna /build/bin/sortmerna /usr/local/bin/sortmerna
ENTRYPOINT ["/usr/local/bin/sortmerna"]
LABEL maintainer='github.com/bschiffthaler'
LABEL software.version=${SORTMERNA_VERSION}
