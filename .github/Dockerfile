ARG ARCH=aarch64
FROM ghcr.io/monkeyx-net/portmaster-build-templates/portmaster-builder:${ARCH}-latest
USER root
RUN apt-get update && apt-get install software-properties-common && add-apt-repository ppa:deadsnakes/ppa -y
RUN apt-get update && apt-get install -y \
    libwayland-bin \
    python3.11 \
    python3.11-venv \
    python3.11-distutils \
    && rm -rf /var/lib/apt/lists/*
RUN python3.11 -m ensurepip --upgrade
RUN python3.11 -m pip install --break-system-packages scons || python3.11 -m pip install scons
COPY dotnet/ /usr/share/dotnet/
ENV DOTNET_ROOT=/usr/share/dotnet
ENV PATH="/usr/share/dotnet:/root/.local/bin:${PATH}"
WORKDIR /workspace
