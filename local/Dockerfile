FROM ubuntu:xenial as planescape

# Install build and dev tools.
RUN apt-get update
RUN apt-get install -y gcc make automake libtool bison flex gcc-multilib g++-multilib git gdb vim telnet
# Install 32-bit libraries
RUN dpkg --add-architecture i386
RUN apt-get update
RUN apt-get install -y libdb5.3++:i386 libdb5.3++-dev:i386 libdb5.3:i386 zlib1g-dev:i386

# Setup home folder
ENV HOME=/home/planescape

# Download and build server code
RUN mkdir ${HOME} && \
cd ${HOME} && \
git clone https://github.com/planescape-mud/planescape_code.git && \
cd planescape_code && \
make -f Makefile.git && \
mkdir ${HOME}/objs && \
cd ${HOME}/objs && \
../planescape_code/configure --prefix=${HOME}/runtime && \
make -j 8 && make install

# Download and install configuration files.
# Set up 'share/world' to point to the local mini-set of areas.
RUN cd ${HOME} && \
git clone https://github.com/planescape-mud/planescape_world.git && \
ln -s ${HOME}/planescape_world ${HOME}/runtime/share && \
ln -s ${HOME}/runtime/share/world.mini ${HOME}/runtime/share/world


# Expose all MUD ports that listen to external connections.
EXPOSE 4000

# Launch MUD on container startup.
CMD cd /home/planescape/runtime && ./bin/planescape etc/planescape.xml

