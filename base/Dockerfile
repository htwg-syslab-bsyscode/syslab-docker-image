FROM ubuntu:22.04

# args
ARG atom_source="https://github.com/atom/atom/releases/download/v1.60.0/atom-amd64.deb"
ARG sublime_source="https://download.sublimetext.com/Sublime%20Text%202.0.2%20x64.tar.bz2"
ENV RUSTUP_HOME=/usr/local/rustup \
    CARGO_HOME=/usr/local/cargo \
    PATH=/usr/local/cargo/bin:$PATH \
    RUST_VERSION=1.62.1 \
    TZ=Europe/Berlin

# install software
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
	apt-transport-https ca-certificates \ 
	openssh-server \
	locales \
	software-properties-common apt-transport-https wget \
	python3-pip \
	hunspell-de-de \
	vim \
	nano \
 	manpages \
     	manpages-dev \
     	htop \
     	curl \
     	tmux \
     	zsh \
     	netcat \
     	tree \
     	git \
     	indent \
     	gist \
     	bats \
     	shellcheck \
     	gcc \
     	clang \
     	cmake \
     	lldb \
     	xsel \
     	gdb \
     	gpg-agent \
     	ddd \
     	valgrind \
     	meld \
     	strace \
     	python3-matplotlib \
     	python-tk \
     	gpg dirmngr gnupg \ 
	build-essential \
	qemu-system libcurses-ocaml-dev zlib1g-dev libc6-dev-arm64-cross gcc-aarch64-linux-gnu gdb-multiarch \
	curl gnupg lsb-release 

# install firefox
RUN add-apt-repository -y ppa:mozillateam/ppa
COPY synchronize/mozilla-firefox /etc/apt/preferences.d/mozilla-firefox
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y firefox

# install sublime_text
RUN curl -fsSL https://download.sublimetext.com/sublimehq-pub.gpg | apt-key add -
RUN add-apt-repository "deb https://download.sublimetext.com/ apt/stable/" -y
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y sublime-text

# install vscode
RUN wget -O- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | tee /usr/share/keyrings/vscode.gpg
RUN echo "deb [arch=amd64 signed-by=/usr/share/keyrings/vscode.gpg] https://packages.microsoft.com/repos/vscode stable main" | tee /etc/apt/sources.list.d/vscode.list
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y code

# install atom
RUN wget "$atom_source"
RUN dpkg -i *deb && rm *deb
RUN mkdir -p /home/syslab/.local/share/applications/
COPY synchronize/atom.desktop /home/syslab/.local/share/applications/

# install rust
RUN set -x && \
    apt-get update --fix-missing && \
    apt-get install -y --no-install-recommends \
    cmake
RUN set -eux; \
    url="https://static.rust-lang.org/rustup/dist/x86_64-unknown-linux-gnu/rustup-init"; \
    wget "$url"; \
    chmod +x rustup-init; \
    ./rustup-init -y --no-modify-path --default-toolchain $RUST_VERSION; \
    rm rustup-init; \
    chmod -R a+w $RUSTUP_HOME $CARGO_HOME; \
    rustup --version; \
    cargo --version; \
    rustc --version;

# install gdbgui
RUN pip3 install gdbgui

#install opencv
RUN apt-get update && apt-get install -y \
	build-essential \
	git \
	pkg-config \
	cmake \
	libgtk2.0-dev \
	libavcodec-dev \
	libavformat-dev \
	libswscale-dev \
	python3-dev \
	python3-numpy \
	libtbb2 \
	libtbb-dev \
	libjpeg-dev \
	libpng-dev \
	libtiff-dev \
	qtbase5-dev qtchooser qt5-qmake qtbase5-dev-tools \
	qtcreator \
	llvm \
	clang \
	libclang-dev \
	libdc1394-dev

RUN mkdir -p /git
RUN cd /git && git clone --single-branch  --branch 4.6.0 https://github.com/opencv/opencv.git
RUN mkdir -p /git/opencv/build
WORKDIR /git/opencv/build
RUN cmake -D CMAKE_BUILD_TYPE=RELEASE \
	-D INSTALL_C_EXAMPLES=OFF \
	-D INSTALL_PYTHON_EXAMPLES=OFF \
	-D WITH_TBB=ON \
	-D WITH_QT=ON \
	-D WITH_OPENGL=ON \
	-D BUILD_EXAMPLES=OFF \
	-D BUILD_TIFF=ON \
	-D OPENCV_GENERATE_PKGCONFIG=ON \
	..

RUN make -j8
RUN make install
RUN ldconfig

# set timezone to Europe/Berlin
RUN apt update && apt install tzdata -y

# env
RUN echo "PATH=$PATH" > /etc/environment
RUN echo "RUSTUP_HOME=$RUSTUP_HOME" >> /etc/environment
RUN echo "CARGO_HOME=$CARGO_HOME" >> /etc/environment
RUN echo "RUST_VERSION=$RUST_VERSION" >> /etc/environment
RUN echo "TZ=$TZ" >> /etc/environment

# set locale / env
RUN locale-gen de_DE de_DE.UTF-8
RUN update-locale LC_ALL=de_DE.UTF-8 LANG=de_DE.UTF-8
ENV LANG="en_US.UTF-8"
ENV LANGUAGE="en_US.UTF-8"
ENV LC_CTYPE="en_US.UTF-8"
ENV LC_MESSAGES="en_US.UTF-8"

ENV LC_MONETARY="de_DE.UTF-8"
ENV LC_NUMERIC="de_DE.UTF-8"
ENV LC_TIME="de_DE.UTF-8"
ENV LC_COLLATE="de_DE.UTF-8"
ENV LC_MONETARY="de_DE.UTF-8"
ENV LC_PAPER="de_DE.UTF-8"
ENV LC_NAME="de_DE.UTF-8"
ENV LC_ADDRESS="de_DE.UTF-8"
ENV LC_TELEPHONE="de_DE.UTF-8"
ENV LC_MEASUREMENT="de_DE.UTF-8"
ENV LC_IDENTIFICATION="de_DE.UTF-8"




