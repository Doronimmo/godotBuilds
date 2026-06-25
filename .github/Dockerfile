ARG ARCH=aarch64
FROM ghcr.io/monkeyx-net/portmaster-build-templates/portmaster-builder:${ARCH}-latest
ARG ARCH
USER root
RUN apt-get update && apt-get install -y libwayland-bin && rm -rf /var/lib/apt/lists/*
COPY deps/ /tmp/deps/
RUN if [ "$ARCH" = "aarch64" ]; then \
        mv /tmp/deps/python3.11 /opt/python3.11 \
        && rm -f /opt/python3.11/pyvenv.cfg \
        && PYTHONHOME=/opt/python3.11 /opt/python3.11/bin/python3 -m ensurepip --upgrade \
        && PYTHONHOME=/opt/python3.11 /opt/python3.11/bin/python3 -m pip install --upgrade pip \
        && (PYTHONHOME=/opt/python3.11 /opt/python3.11/bin/python3 -m pip install --break-system-packages scons \
            || PYTHONHOME=/opt/python3.11 /opt/python3.11/bin/python3 -m pip install scons); \
    else \
        apt-get update && apt-get install -y software-properties-common && add-apt-repository ppa:deadsnakes/ppa -y \
        && apt-get update && apt-get install -y python3.11 python3.11-venv python3.11-distutils && rm -rf /var/lib/apt/lists/* \
        && python3.11 -m ensurepip --upgrade \
        && (python3.11 -m pip install --break-system-packages scons || python3.11 -m pip install scons); \
    fi \
    && rm -rf /tmp/deps
COPY dotnet/ /usr/share/dotnet/
ENV DOTNET_ROOT=/usr/share/dotnet
ENV PATH="/usr/share/dotnet:/root/.local/bin:${PATH}"
WORKDIR /workspace
