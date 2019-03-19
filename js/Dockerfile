FROM davefinster/coder:usermode

RUN curl -O https://nodejs.org/dist/v10.15.3/node-v10.15.3-linux-x64.tar.xz && \
	tar xf node-v10.15.3-linux-x64.tar.xz && \
	sudo mv node-v10.15.3-linux-x64 /node && \
	rm -rf node-v10.15.3-linux-x64.tar.xz

ENV PATH "$PATH:/node/bin"

ENTRYPOINT ["code-server"];
