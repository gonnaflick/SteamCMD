FROM ubuntu:latest

LABEL maintainer="a338906@uach.mx" \
      name="SteamCMD" \
      version="1.0"

ENV USER steam
ENV HOMEDIR /home/${USER}
ENV STEAMCMDDIR ${HOMEDIR}/steamcmd

# Install the necessary dependencies and configurations.
RUN dpkg --add-architecture i386
RUN apt-get update && apt-get -y install sudo \
      curl git wget file tar bzip2 gzip unzip bsdmainutils python3 \
      util-linux ca-certificates binutils bc jq tmux netcat screen \
      lib32gcc-s1 cpio distro-info xz-utils lib32stdc++6 libsdl2-2.0-0:i386 \
      lib32z1 coreutils iputils-ping iproute2 locales nano \
      && sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen

# Create the steam user, include it in the list of sudoers.
# Remove steam user password whenever sudo.
RUN adduser --disabled-password --gecos '' ${USER} \
      && usermod -aG sudo ${USER} \
      && echo "${USER} ALL=(ALL) NOPASSWD:ALL" | EDITOR='tee -a' visudo

# Install SteamCMD manually
RUN su - steam -c \
      "mkdir -p "${STEAMCMDDIR}/" \
      && wget -qO- 'https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz' | tar xvzf - -C "${STEAMCMDDIR}/" \
      && "${STEAMCMDDIR}/steamcmd.sh" +quit \
      && mkdir -p "${HOMEDIR}/.steam/sdk32" \
      && ln -s "${STEAMCMDDIR}/linux32/steamclient.so" "${HOMEDIR}/.steam/sdk32/steamclient.so" \
      && ln -s "${STEAMCMDDIR}/linux32/steamcmd" "${STEAMCMDDIR}/linux32/steam" \
      && ln -s "${STEAMCMDDIR}/steamcmd.sh" "${STEAMCMDDIR}/steam.sh""

# Switch to steam and its work directory
USER ${USER}
WORKDIR ${HOMEDIR}
