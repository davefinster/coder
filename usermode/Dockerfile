FROM davefinster/coder:official-vscode

RUN code --user-data-dir=/root --install-extension zhuangtongfa.material-theme && \
	code --user-data-dir=/root --install-extension zxh404.vscode-proto3

FROM codercom/code-server

RUN apt-get update && \
	apt-get install -y locales net-tools curl build-essential git sudo unzip && \
	adduser --disabled-password --ingroup sudo -u 3000 --gecos '' code && \
	echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers && \
	echo "user ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/user && \
	chmod 0440 /etc/sudoers.d/user && \
	locale-gen en_US.UTF-8  && \
	curl -L -O https://github.com/google/protobuf/releases/download/v3.6.0/protoc-3.6.0-linux-x86_64.zip && \
	unzip protoc-3.6.0-linux-x86_64.zip && \
	mv bin/protoc /usr/local/bin/protoc && \
	mv include/* /usr/local/include && \
	rm -rf protoc-3.6.0-linux-x86_64.zip bin include readme.txt

USER code
WORKDIR /home/code
RUN mkdir /home/code/.code-server && \
	mkdir -p /home/code/.code-server/User && \
	mkdir -p /home/code/.code-server/extensions && \
	mkdir projects

COPY --from=0 /root/.vscode/extensions /home/code/.code-server/extensions

COPY ./settings.json /home/code/.code-server/User/settings.json

RUN sudo chown -R 3000 .code-server

ENTRYPOINT ["dumb-init", "code-server"]
