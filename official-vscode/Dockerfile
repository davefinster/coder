FROM ubuntu:16.04

ENV LANG=C.UTF-8 \
    DEBIAN_FRONTEND=noninteractive \
    DEBCONF_NONINTERACTIVE_SEEN=true \
    VSCODE=https://vscode-update.azurewebsites.net/latest/linux-deb-x64/stable \
    TINI_VERSION=v0.16.1


RUN apt-get update -qq && \
    echo 'Installing OS dependencies' && \
    apt-get install -qq -y --fix-missing sudo software-properties-common libxext-dev libxrender-dev libxslt1.1 libgconf-2-4 libnotify4 libnspr4 libnss3 libnss3-nssdb libxtst-dev libgtk2.0-0 libcanberra-gtk-module libxss1 libxkbfile1 git curl tree locate net-tools telnet emacs ruby make bash-completion bash-completion python python-pip meld nodejs-legacy npm libxkbfile1 libxss1 locales netcat && \
    echo 'Cleaning up' && \
    apt-get clean -qq -y && \
    apt-get autoclean -qq -y && \
    apt-get autoremove -qq -y &&  \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/* && \
    updatedb && \
    locale-gen en_US.UTF-8

RUN echo 'Installing VsCode' && \
    curl -o vscode.deb -J -L "$VSCODE" && \
    dpkg -i vscode.deb && rm -f vscode.deb && \
    echo "Install OK"

CMD ["bash"]
