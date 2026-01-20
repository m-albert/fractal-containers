FROM ghcr.io/fractal-analytics-platform/ubuntu24-slurm-multipy:0.1

ARG FRACTAL_SERVER_VERSION
ARG SLURM_CPUS
ARG SLURM_MEMORY

RUN sed -i "s/CPUs=[0-9]*/CPUs=${SLURM_CPUS}/g" /etc/slurm/slurm.conf
RUN sed -i "s/RealMemory=[0-9]*/RealMemory=${SLURM_MEMORY}/g" /etc/slurm/slurm.conf

# Create the albertm user for slurm_sudo with matching UID/GID from host
RUN groupadd -g 1029 albertm && \
    useradd -m -u 650186 -g 1029 -s /bin/bash albertm && \
    echo "albertm ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

RUN mkdir -p /data/app/Tasks
RUN mkdir -p /data/app/Artifacts

RUN echo "Install fractal-server ${FRACTAL_SERVER_VERSION}"
RUN python3 -m venv /venv-server
RUN /venv-server/bin/python3 -m pip install fractal-server==${FRACTAL_SERVER_VERSION}


COPY run_server.sh ./
COPY .fractal_server.env ./
COPY profile.json ./
COPY resource.json ./

ENTRYPOINT ["bash", "run_server.sh"]
