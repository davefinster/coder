FROM davefinster/coder:official-vscode

RUN code --user-data-dir=/root --install-extension ms-vscode.go

FROM davefinster/coder:base

WORKDIR /home/coder

RUN curl -O https://dl.google.com/go/go1.14.2.linux-amd64.tar.gz && \
	sudo tar -C /usr/local -xzf go1.14.2.linux-amd64.tar.gz && \
	rm go1.14.2.linux-amd64.tar.gz && \
	curl -O -L https://github.com/golang-migrate/migrate/releases/download/v4.10.0/migrate.linux-amd64.tar.gz && \
	tar -zxvf migrate.linux-amd64.tar.gz && \
	sudo mv migrate/migrate.linux-amd64 /usr/local/bin/migrate && \
	rm migrate.linux-amd64.tar.gz

COPY --from=0 /root/.vscode/extensions /home/coder/.local/share/code-server/extensions

ENV PATH "$PATH:/home/coder/go/bin:/usr/local/go/bin"
ENV GOPATH "/home/coder/go"

COPY ./settings.json /home/coder/.local/share/code-server/User/settings.json

RUN mkdir -p ./go && \
	go get -u github.com/stamblerre/gocode && \
	mv ./go/bin/gocode ./go/bin/gocode-gomod && \
	go get -u github.com/mdempsky/gocode && \
	go get -u github.com/ramya-rao-a/go-outline && \
	go get -u github.com/newhook/go-symbols && \
	go get -u github.com/uudashr/gopkgs/cmd/gopkgs && \
	go get -u golang.org/x/tools/cmd/guru && \
	go get -u golang.org/x/tools/cmd/gorename && \
	go get -u golang.org/x/tools/cmd/goimports && \
	go get -u github.com/rogpeppe/godef && \
	go get -u golang.org/x/tools/cmd/godoc && \
	go get -u golang.org/x/lint/golint && \
	go get -u github.com/go-delve/delve/cmd/dlv && \
	go get -u github.com/sqs/goreturns && \
	go get -u github.com/golang/protobuf/protoc-gen-go && \
    GO111MODULE=on go get golang.org/x/tools/gopls@latest && \
	sudo chown -R coder /home/coder/.local/share/code-server/extensions && \
	curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh && \
    sudo chown -R coder /home/coder/.local

WORKDIR /home/coder/project
