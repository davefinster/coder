FROM davefinster/coder:official-vscode

RUN code --user-data-dir=/root --install-extension golang.go

FROM davefinster/coder:base

WORKDIR /home/coder

ENV GO_VERSION=1.15.2 \
    GOOS=linux \
    GOARCH=amd64 \
    GOROOT=/home/coder/go \
    GOPATH=/home/coder/go/tools

ENV PATH=$GOPATH/bin:$GOROOT/bin:$PATH

RUN curl -fsSL https://storage.googleapis.com/golang/go$GO_VERSION.$GOOS-$GOARCH.tar.gz | tar -C /home/coder -xzv && \
    curl -O -L https://github.com/golang-migrate/migrate/releases/download/v4.12.2/migrate.linux-amd64.tar.gz && \
	tar -zxvf migrate.linux-amd64.tar.gz && \
	sudo mv migrate.linux-amd64 /usr/local/bin/migrate && \
	rm migrate.linux-amd64.tar.gz

COPY --from=0 /root/.vscode/extensions /home/coder/.local/share/code-server/extensions

ENV PATH "$PATH:/home/coder/go/bin"

COPY ./settings.json /home/coder/.local/share/code-server/User/settings.json

RUN sudo chown -R coder /home/coder/.local && \
    go get -u -v google.golang.org/protobuf/cmd/protoc-gen-go && \
    export GO111MODULE=on && \
    go get -v -u golang.org/x/tools/gopls@latest && \
    go get -v -u github.com/uudashr/gopkgs@latest && \
    go get -v -u github.com/ramya-rao-a/go-outline@latest && \
    go get -v -u github.com/rogpeppe/godef@latest && \
    go get -v -u github.com/sqs/goreturns@latest && \
    go get -v -u golang.org/x/lint/golint@latest && \
    go get -v -u github.com/uudashr/gopkgs/v2/cmd/gopkgs && \
    go get -v -u github.com/stamblerre/gocode && \
    cp /home/coder/go/tools/bin/gocode /home/coder/go/tools/bin/gocode-gomod && \
    go get -v github.com/go-delve/delve/cmd/dlv

WORKDIR /home/coder/project
