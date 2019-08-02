FROM davefinster/coder:official-vscode

RUN code --user-data-dir=/root --install-extension zhuangtongfa.material-theme && \
	code --user-data-dir=/root --install-extension zxh404.vscode-proto3

FROM codercom/code-server

WORKDIR /home/coder

RUN sudo apt-get update && \
	sudo apt-get install -y locales net-tools curl build-essential git sudo unzip && \
	sudo locale-gen en_US.UTF-8  && \
	curl -L -O https://github.com/google/protobuf/releases/download/v3.6.0/protoc-3.6.0-linux-x86_64.zip && \
	unzip protoc-3.6.0-linux-x86_64.zip && \
	sudo mv bin/protoc /usr/local/bin/protoc && \
	sudo mv include/* /usr/local/include && \
	rm -rf protoc-3.6.0-linux-x86_64.zip bin include readme.txt

RUN mkdir ./.code-server && \
	mkdir -p ./.code-server/User && \
	mkdir -p ./.code-server/extensions

COPY --from=0 /root/.vscode/extensions ./.code-server/extensions

COPY ./settings.json .code-server/User/settings.json

RUN sudo chown -R coder ./.code-server

WORKDIR /home/coder/project

ENTRYPOINT ["dumb-init", "code-server"]
