FROM davefinster/coder:official-vscode

RUN code --user-data-dir=/root --install-extension James-Yu.latex-workshop

FROM davefinster/coder:base

WORKDIR /home/coder

COPY --from=0 /root/.vscode/extensions ./.code-server/extensions

RUN sudo apt-get update && sudo apt-get -y install software-properties-common && \
    sudo add-apt-repository ppa:jonathonf/texlive && \
    export DEBIAN_FRONTEND=noninteractive && \
    sudo apt-get install -y tzdata && \
    sudo apt-get update && sudo apt-get install -y texlive-full && \
    sudo chown -R coder ./.code-server

WORKDIR /home/coder/project
