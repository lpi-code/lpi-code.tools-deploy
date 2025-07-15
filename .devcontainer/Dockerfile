FROM mcr.microsoft.com/devcontainers/python:3.12-bookworm



# copies the requirements file from the project root to the container and installs it
# copy "noop.txt" so the COPY instruction does not fail if no requirements.txt exists.
COPY requirements.txt* .devcontainer/noop.txt /tmp/pip-tmp/
RUN if [ -f "/tmp/pip-tmp/requirements.txt" ]; then pip3 --disable-pip-version-check --no-cache-dir install -r /tmp/pip-tmp/requirements.txt; fi \
    && rm -rf /tmp/pip-tmp

RUN mkdir -p /ansible_collections/lpi_code/tools_deploy

RUN useradd vscode; \
echo vscode:10000:5000 > /etc/subuid; \
echo vscode:10000:5000 > /etc/subgid;

RUN apt update \
    && apt install -y wget \
    && wget http://downloadcontent.opensuse.org/repositories/home:/alvistack/Debian_12/Release.key -O alvistack_key \
    && cat alvistack_key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/alvistack.gpg  >/dev/null \
    && apt install -y podman podman-docker \
    && apt remove -y wget
WORKDIR /workspace