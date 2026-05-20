ARG ARCH=aarch64
FROM ghcr.io/monkeyx-net/portmaster-build-templates/portmaster-builder:${ARCH}-latest
USER root
RUN apt-get update && apt-get install -y \
    libwayland-bin \
    python3 \
    python3-pip \
    && rm -rf /var/lib/apt/lists/*
RUN pip3 install --break-system-packages scons || pip3 install scons
COPY dotnet/ /usr/share/dotnet/
ENV DOTNET_ROOT=/usr/share/dotnet
ENV PATH="/usr/share/dotnet:/root/.local/bin:${PATH}"
WORKDIR /workspace