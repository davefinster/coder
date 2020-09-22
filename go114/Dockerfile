FROM davefinster/coder:official-vscode

RUN code --user-data-dir=/root --install-extension golang.go

FROM davefinster/coder:base

WORKDIR /home/coder

ENV GO_VERSION=1.15.2 \
    GOOS=linux \
    GOARCH=amd64 \
    GOROOT=/home/coder/go \
    GOPATH=/home/coder/go-tools \
    GO111MODULE=on
ENV PATH=$GOPATH/bin:$GOROOT/bin:$PATH

RUN curl -fsSL https://storage.googleapis.com/golang/go$GO_VERSION.$GOOS-$GOARCH.tar.gz | tar -C /home/coder -xzv && \
    curl -O -L https://github.com/golang-migrate/migrate/releases/download/v4.12.2/migrate.linux-amd64.tar.gz && \
	tar -zxvf migrate.linux-amd64.tar.gz && \
	sudo mv migrate.linux-amd64 /usr/local/bin/migrate && \
	rm migrate.linux-amd64.tar.gz

COPY --from=0 /root/.vscode/extensions /home/coder/.local/share/code-server/extensions

ENV PATH "$PATH:/home/coder/go/bin:/usr/local/go/bin"

COPY ./settings.json /home/coder/.local/share/code-server/User/settings.json

RUN mkdir -p ./go && \
    go get -u github.com/stamblerre/gocode && \
	cp $GOPATH/bin/gocode $GOPATH/bin/gocode-gomod && \
    go get -u -v golang.org/x/tools/gopls@latest && \
    go get -u -v google.golang.org/protobuf/cmd/protoc-gen-go && \
    go get -u -v github.com/uudashr/gopkgs/cmd/gopkgs@v2 && \
    go get -u -v github.com/ramya-rao-a/go-outline && \
    go get -u -v github.com/acroca/go-symbols && \
    go get -u -v golang.org/x/tools/cmd/guru && \
    go get -u -v golang.org/x/tools/cmd/gorename && \
    go get -u -v github.com/fatih/gomodifytags && \
    go get -u -v github.com/haya14busa/goplay/cmd/goplay && \
    go get -u -v github.com/josharian/impl && \
    go get -u -v github.com/tylerb/gotype-live && \
    go get -u -v github.com/rogpeppe/godef && \
    go get -u -v github.com/zmb3/gogetdoc && \
    go get -u -v golang.org/x/tools/cmd/goimports && \
    go get -u -v github.com/sqs/goreturns && \
    go get -u -v winterdrache.de/goformat/goformat && \
    go get -u -v golang.org/x/lint/golint && \
    go get -u -v github.com/cweill/gotests/... && \
    go get -u -v honnef.co/go/tools/... && \
    go get -v github.com/golangci/golangci-lint/cmd/golangci-lint@v1.27.0 && \
    go get -u -v github.com/mgechev/revive && \
    go get -u -v github.com/sourcegraph/go-langserver && \
    go get -v github.com/go-delve/delve/cmd/dlv && \
    go get -u -v github.com/davidrjenni/reftools/cmd/fillstruct && \
    go get -u -v github.com/godoctor/godoctor && \
	sudo chown -R coder /home/coder/.local/share/code-server/extensions && \
    sudo chown -R coder /home/coder/.local

WORKDIR /home/coder/project
