FROM davefinster/coder:usermode

RUN curl -O https://nodejs.org/dist/v10.15.3/node-v10.15.3-linux-x64.tar.xz && \
	tar xf node-v10.15.3-linux-x64.tar.xz && \
	sudo mv node-v10.15.3-linux-x64 /node && \
	rm -rf node-v10.15.3-linux-x64.tar.xz && \
	curl -L -O https://github.com/grpc/grpc-web/releases/download/1.0.4/protoc-gen-grpc-web-1.0.4-linux-x86_64 && \
	sudo mv protoc-gen-grpc-web-1.0.4-linux-x86_64 /usr/local/bin/protoc-gen-grpc-web && \
	sudo chmod +x /usr/local/bin/protoc-gen-grpc-web

ENV PATH "$PATH:/node/bin"

ENTRYPOINT ["dumb-init", "code-server"]
