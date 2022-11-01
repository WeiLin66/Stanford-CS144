# Standford CS 144: Introduction to Computer Networking

## Resources

[Official Website](https://cs144.github.io/)

[Video](https://www.youtube.com/playlist?list=PL6RdenZrxrw9inR-IJv-erlOKRHjymxMN)

## Prerequisite

[Setting up your CS144 VM using VirtualBox](https://stanford.edu/class/cs144/vm_howto/vm-howto-iso.html)

[Linux Packages installation Guide](https://stanford.edu/class/cs144/vm_howto/vm-howto-byo.html)

**setup_dev_env.sh**

```shell
#!/bin/sh

if [ -z "$SUDO_USER" ]; then
    # if the user didn't call us with sudo, re-execute
    exec sudo $0 "$@"
fi

### update sources and get add-apt-repository
apt-get update
apt-get -y install software-properties-common

### add the extended source repos
add-apt-repository multiverse
add-apt-repository universe
add-apt-repository restricted

### make sure we're totally up-to-date now
apt-get update
apt-get -y dist-upgrade

### install the software we need for the VM and build env
apt-get -y install build-essential gcc gcc-8 g++ g++-8 cmake libpcap-dev htop jnettop screen   \
                   emacs-nox vim-nox automake pkg-config libtool libtool-bin git tig links     \
                   parallel iptables mahimahi mininet net-tools tcpdump wireshark telnet socat \
                   clang clang-format clang-tidy clang-tools coreutils bash doxygen graphviz   \
                   virtualbox-guest-utils netcat-openbsd

## make a sane set of alternatives for gcc, and make gcc-8 the default
# GCC
update-alternatives --remove-all gcc &>/dev/null
for ver in 7 8; do
    update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-${ver} $((10 * ${ver})) \
        $(for prog in g++ gcc-ar gcc-nm gcc-ranlib gcov gcov-dump gcov-tool; do
            echo "--slave /usr/bin/${prog} ${prog} /usr/bin/${prog}-${ver}"
        done)
done

### add user to the virtualbox shared folder group and enable the virtualbox guest utils
adduser "$SUDO_USER" vboxsf
systemctl enable virtualbox-guest-utils.service
```

## Labs

- [ ] [Checkpoint 0: networking warmup](https://cs144.github.io/assignments/lab0.pdf)
- [ ] [Checkpoint 1: stitching substrings into a byte stream](https://cs144.github.io/assignments/lab1.pdf)
- [ ] [Checkpoint 2: the TCP receiver](https://cs144.github.io/assignments/lab2.pdf)
- [ ] [Checkpoint 3: the TCP sender](https://cs144.github.io/assignments/lab3.pdf)
- [ ] [Checkpoint 4: the TCP connection](https://cs144.github.io/assignments/lab4.pdf)
- [ ] [Checkpoint 5: the network interface](https://cs144.github.io/assignments/lab5.pdf)
- [ ] [Checkpoint 6: the IP router](https://cs144.github.io/assignments/lab6.pdf)
- [ ] [Checkpoint 7: putting it all together](https://cs144.github.io/assignments/lab7.pdf)  