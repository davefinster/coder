FROM davefinster/coder:official-vscode

RUN code --user-data-dir=/root --install-extension ms-vscode.go

FROM davefinster/coder:usermode

RUN curl -O https://dl.google.com/go/go1.12.linux-amd64.tar.gz && \
	sudo tar -C /usr/local -xzf go1.12.linux-amd64.tar.gz && \
	rm go1.12.linux-amd64.tar.gz 

COPY --from=0 /root/.vscode/extensions /home/code/.code-server/extensions

ENV PATH "$PATH:/home/code/go/bin:/usr/local/go/bin"
ENV GOPATH "/home/code/go"

RUN mkdir -p /home/code/go && \
	go get -u github.com/stamblerre/gocode && \
	mv /home/code/go/bin/gocode /home/code/go/bin/gocode-gomod && \
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
	sudo chown -R 3000 .code-server && \
	curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh

