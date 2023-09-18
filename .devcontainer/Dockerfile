FROM python:3.8

# Set non-root user arguments
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Create a non-root user
RUN apt-get update && apt-get -y install sudo \
    && groupadd --gid ${USER_GID} ${USERNAME} \
    && useradd -s /bin/bash --uid ${USER_UID} --gid ${USER_GID} -m ${USERNAME} \
    && echo ${USERNAME} ALL=\(ALL\) NOPASSWD:ALL > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME} \
    # Install necessary dependencies
    && apt-get install -y pypy3 nodejs npm \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install the packages listed in requirements.txt
COPY requirements.txt /tmp/
RUN python -m pip install --upgrade pip \
    && pip install -r /tmp/requirements.txt

# Install the packages for atcoder
RUN pip install online-judge-tools \
    && npm install -g atcoder-cli
