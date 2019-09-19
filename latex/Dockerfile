FROM davefinster/coder:official-vscode

RUN code --user-data-dir=/root --install-extension James-Yu.latex-workshop

FROM davefinster/coder:base

WORKDIR /home/coder

COPY --from=0 /root/.vscode/extensions ./.code-server/extensions

RUN sudo add-apt-repository ppa:jonathonf/texlive && \
    sudo apt update && sudo apt install texlive-full && \
    sudo chown -R coder ./.code-server

WORKDIR /home/coder/project
