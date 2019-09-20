FROM davefinster/coder:official-vscode

RUN curl -O https://marketplace.visualstudio.com/_apis/public/gallery/publishers/James-Yu/vsextensions/latex-workshop/6.5.1/vspackage && \
    cat vspackage | gunzip > latex-workshop.vsix && \
    code --user-data-dir=/root --install-extension latex-workshop.vsix

FROM davefinster/coder:base

WORKDIR /home/coder

COPY --from=0 /root/.vscode/extensions ./.code-server/extensions

RUN sudo apt-get update && sudo apt-get -y install software-properties-common && \
    sudo add-apt-repository ppa:jonathonf/texlive && \
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y tzdata && \
    sudo apt-get update && sudo apt-get install -y texlive-full fonts-roboto && \
    sudo chown -R coder ./.code-server

WORKDIR /home/coder/project
