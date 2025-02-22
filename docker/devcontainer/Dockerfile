# [Choice] Debian / Ubuntu version (use Debian 12, Debian 11, Ubuntu 22.04 on local arm64/Apple Silicon): debian-12, debian-11, debian-10, ubuntu-22.04, ubuntu-20.04
# https://mcr.microsoft.com/v2/vscode/devcontainers/base/tags/list
ARG VARIANT=ubuntu-24.04
FROM mcr.microsoft.com/devcontainers/base:${VARIANT}
USER root

# Install needed packages. Use a separate RUN statement to add your own dependencies.
RUN apt-get update
RUN export DEBIAN_FRONTEND=noninteractive && apt-get -y install build-essential cppcheck valgrind clang lldb llvm gdb
RUN export DEBIAN_FRONTEND=noninteractive && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/*
RUN wget -qO- "https://github.com/Kitware/CMake/releases/download/v3.28.1/cmake-3.28.1-linux-x86_64.tar.gz" | tar --strip-components=1 -xz -C /usr/local

# Install Docker
# Add Docker's official GPG key:
RUN apt-get update
RUN apt-get install -y ca-certificates curl
RUN install -m 0755 -d /etc/apt/keyrings
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
RUN chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
RUN echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  tee /etc/apt/sources.list.d/docker.list > /dev/null

RUN apt-get update && apt-get install -y libspdlog-dev libfmt-dev libboost-stacktrace-dev docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

ARG USERNAME=vscode
RUN mkdir -p /home/"${USERNAME}/.docker"
RUN chown "${USERNAME}":"${USERNAME}" /home/"${USERNAME}" -R
RUN chmod g+rwx "/home/${USERNAME}/.docker" -R

RUN gpasswd -a ${USERNAME} docker

# Setup ENV vars for vcpkg
ENV VCPKG_ROOT=/usr/local/vcpkg \
    VCPKG_DOWNLOADS=/usr/local/vcpkg-downloads
ENV PATH="${PATH}:${VCPKG_ROOT}"

RUN echo "export PATH=/usr/local/cmake-3.28.1-linux-x86_64/bin:$PATH" >> ~.bash_rc

# Install vcpkg itself: https://github.com/microsoft/vcpkg/blob/master/README.md#quick-start-unix
COPY base-scripts/install-vcpkg.sh /tmp/
RUN chmod +x /tmp/install-vcpkg.sh \
    && ./tmp/install-vcpkg.sh ${USERNAME} \
    && rm -f /tmp/install-vcpkg.sh

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

ENTRYPOINT ["sudo", "service", "docker", "start", "&&", "sleep", "5", "&&", "sudo", "chown", "${USERNAME}", "/var/run/docker.sock", "&&", "/bin/bash"]
