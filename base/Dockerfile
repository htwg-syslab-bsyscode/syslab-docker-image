FROM ubuntu:22.04

# args
ARG atom_source="https://github.com/atom/atom/releases/download/v1.60.0/atom-amd64.deb"
ARG sublime_source="https://download.sublimetext.com/Sublime%20Text%202.0.2%20x64.tar.bz2"

# install software
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
	apt-transport-https ca-certificates \ 
	openssh-server \
	locales \
	software-properties-common apt-transport-https wget \
	python3-pip \
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

# set timezone to Europe/Berlin
RUN apt update && apt install tzdata -y
ENV TZ="Europe/Berlin"

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




