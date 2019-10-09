FROM davefinster/coder:go

WORKDIR /home/coder

COPY ./settings.json /home/coder/.local/share/code-server/User/settings.json

RUN GO111MODULE=on go get golang.org/x/tools/gopls@latest && \
    sudo chown -R coder /home/coder/.local

WORKDIR /home/coder/project
