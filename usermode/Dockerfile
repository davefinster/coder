FROM davefinster/coder:official-vscode

RUN code --user-data-dir=/root --install-extension zhuangtongfa.material-theme

FROM codercom/code-server

RUN apt-get update && \
	apt-get install -y locales net-tools curl build-essential git sudo && \
	adduser --disabled-password --ingroup sudo -u 3000 --gecos '' coder && \
	echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers && \
	echo "user ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/user && \
	chmod 0440 /etc/sudoers.d/user && \
	locale-gen en_US.UTF-8 

USER coder
WORKDIR /home/coder
RUN mkdir /home/coder/.code-server && \
	mkdir -p /home/coder/.code-server/extensions && \
	mkdir projects

COPY --from=0 /root/.vscode/extensions /home/coder/.code-server/extensions

RUN sudo chown -R 3000 .code-server

ENTRYPOINT ["code-server"]
