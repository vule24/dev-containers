FROM jupyter/pyspark-notebook:latest

USER root
RUN echo "${NB_USER} ALL=(ALL:ALL) NOPASSWD:ALL" > /etc/sudoers.d/${NB_USER}
# Install dependencies / Set environment variables as root here

USER ${NB_USER}
# Install dependencies / Set environment variables as user here
COPY environment.yml /tmp/environment.yml
RUN mamba env update --file /tmp/environment.yml && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

COPY overrides.json /opt/conda/share/jupyter/lab/settings/

WORKDIR /home/${NB_USER}/work

ENV JUPYTER_TOKEN 123
