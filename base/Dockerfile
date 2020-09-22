FROM davefinster/coder:official-vscode

RUN code --user-data-dir=/root --install-extension zhuangtongfa.material-theme && \
	code --user-data-dir=/root --install-extension zxh404.vscode-proto3

FROM codercom/code-server:3.5.0

WORKDIR /home/coder

RUN sudo apt-get update && \
	sudo apt-get install --fix-missing -y locales net-tools curl build-essential git sudo unzip wget && \
	sudo locale-gen en_US.UTF-8  && \
    curl -L -O  https://github.com/protocolbuffers/protobuf/releases/download/v3.13.0/protoc-3.13.0-linux-x86_64.zip && \
	unzip protoc-3.13.0-linux-x86_64.zip && \
	sudo mv bin/protoc /usr/local/bin/protoc && \
	sudo mv include/* /usr/local/include && \
	rm -rf protoc-3.13.0-linux-x86_64.zip bin include readme.txt && \
	echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] http://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
	curl https://packages.cloud.google.com/apt/doc/apt-key.gpg > /tmp/googlekey.key && \
	sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add /tmp/googlekey.key && \
	sudo apt-get update && \
	sudo apt-get install -y google-cloud-sdk kubectl && \
	wget -q -O /tmp/libpng12.deb http://mirrors.kernel.org/ubuntu/pool/main/libp/libpng/libpng12-0_1.2.54-1ubuntu1_amd64.deb && \
  	sudo dpkg -i /tmp/libpng12.deb && \
  	rm /tmp/libpng12.deb && \
	curl -O https://download.docker.com/linux/static/stable/x86_64/docker-19.03.9.tgz && \
	tar -zxvf docker-19.03.9.tgz && \
	sudo mv docker/docker /usr/local/bin/docker && \
	rm -rf docker && \
	rm -rf docker-19.03.9.tgz

RUN mkdir -p /home/coder/.local/share/code-server/extensions && \
	mkdir -p /home/coder/.local/share/code-server/User

COPY --from=0 /root/.vscode/extensions /home/coder/.local/share/code-server/extensions

COPY ./settings.json /home/coder/.local/share/code-server/User/settings.json

RUN mkdir -p /home/coder/project && \
    sudo chown -R coder /home/coder/.local && \
    sudo chown -R coder /home/coder/project

WORKDIR /home/coder/project

ENTRYPOINT ["/usr/bin/entrypoint.sh", "--bind-addr", "0.0.0.0:8080", "--auth", "none", "."]
