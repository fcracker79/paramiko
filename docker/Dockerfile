FROM ubuntu:12.04
RUN apt-get update && apt-get install -y libssl0.9.8 git cmake gcc g++ make zlib1g-dev libgcrypt-dev openssl libssl-dev vim
WORKDIR /opt/
RUN git clone git://git.libssh.org/projects/libssh.git libssh
WORKDIR /opt/libssh
RUN git checkout v0-6
WORKDIR /opt/libssh/build
RUN cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Debug ..
RUN make && make install && ldconfig
COPY dino.c /opt/libssh/build
RUN gcc dino.c -lssh -lssl -o dino
RUN ssh-keygen -f ssh_host_rsa_key -N '' -t rsa
RUN ssh-keygen -f ssh_host_dsa_key -N '' -t dsa
RUN ssh-keygen -f ssh_host_ecdsa_key -N '' -t ecdsa -b 521

ENTRYPOINT ["./dino", "-p", "2222", "-r", "ssh_host_rsa_key", "-d", "ssh_host_dsa_key", "-k", "ssh_host_ecdsa_key", "0.0.0.0" ]
