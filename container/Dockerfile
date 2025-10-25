FROM fedora:43 AS builder

WORKDIR /opt/geyser
RUN dnf install -y wget2-wget \
    && wget2 --quiet --output-document "Geyser-Standalone.jar" "https://download.geysermc.org/v2/projects/geyser/versions/latest/builds/latest/downloads/standalone"

FROM fedora:43 AS runner

WORKDIR /opt/geyser
RUN dnf install -y java-25-openjdk-headless

COPY --from=builder /opt/geyser /opt/geyser
COPY run.sh /opt/geyser
RUN chmod +x run.sh

# Preload Geyjer configs
RUN ./run.sh & pid=$! \
    && sleep 30 \
    && kill $pid || true

CMD ["/opt/geyser/run.sh"]