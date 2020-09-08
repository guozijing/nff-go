# nff-go
README of nff-go
### nff-go README


####  git clone for nff-go

- git clone --recurse-submodules http://github.com/intel-go/nff-go

#### install deps of nff-go

- apt install liblua5.3-dev libmnl-dev libelf-dev libnuma-dev build-essential libibverbs-dev
- pip3 install meson ninja


- git clone https://github.com/libbpf/libbpf.git
- cd libbpf/src
- make
- sudo make install
- echo "/usr/lib64" >> /etc/ld.so.conf
- ldconfig  &emsp; **(root)**
- cp -rf ./libbpf/include/uapi/linux PATH_NFFGO/nff-go/internal/low/


#### install Go1.14

- wget https://dl.google.com/go/go1.14.4.linux-amd64.tar.gz
- tar -xvf go1.14.4.linux-amd64.tar.gz -C /usr/local/
- export PATH=$PATH:/usr/local/go/bin
- Check by "go version"

#### Hugepages

- PATH_NFFGO/nff-go/dpdk/dpdk/usertools
- dpdk-setup.sh   &emsp;  &emsp; _input **47** and a **number** for hugepages, then input **60** for quit_

#### compile DPDK

- cd nff-go/dpdk/dpdk/
- meson build
- cd build
- ninja
- ninja install  &emsp; **(root)**
- ldconfig &emsp; **(root)**

#### compile nff-go

- cd nff-go
- go mod download 
- make -j8

##### run DPDK helloworld

- cd ../examples/helloworld/
- export RTE_SDK=PATH_NFFGO/nff-go/dpdk/dpdk/
- export RTE_TARGET=x86_64-native-linuxapp-gcc
- make
- cd build
- sudo ./helloworld

#### test nff-go

- make testing &emsp; **(root)**
