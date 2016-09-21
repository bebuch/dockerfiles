FROM gcc:latest

ENV LLVM_VERSION_1 3
ENV LLVM_VERSION_2 9
ENV LLVM_VERSION_3 0

# combine version
ENV LLVM_VERSION $LLVM_VERSION_1.$LLVM_VERSION_2.$LLVM_VERSION_3

# set aliases
ENV LLVM_GPG http://llvm.org/releases/$LLVM_VERSION_1.8.0
ENV LLVM_DOWNLOAD http://llvm.org/releases/$LLVM_VERSION
ENV LLVM_TAR clang+llvm-$LLVM_VERSION-x86_64-linux-gnu-debian8.tar.xz

# download and install llvm
RUN curl -fSL "$LLVM_GPG/hans-gpg-key.asc" -o key.gpg \
	&& gpg --import key.gpg && rm key.gpg \
	&& curl -fSL \
	"https://pgp.mit.edu/pks/lookup?op=get&search=0x8F0871F202119294" \
	-o key.gpg && gpg --import key.gpg && rm key.gpg \
	&& curl -fSL "$LLVM_DOWNLOAD/$LLVM_TAR" -o llvm.tar.xz \
	&& curl -fSL "$LLVM_DOWNLOAD/$LLVM_TAR.sig" -o llvm.tar.xz.sig \
	&& ls -l \
	&& gpg --batch --verify llvm.tar.xz.sig llvm.tar.xz \
	&& mkdir -p /usr/llvm \
	&& tar -xf llvm.tar.xz -C /usr/llvm --strip-components=1 \
	&& rm llvm.tar.xz*

ENV PATH $PATH:/usr/llvm/bin

# llvm installs .so files in /usr/llvm/lib...
RUN echo '/usr/llvm/lib' > /etc/ld.so.conf.d/local-llvm.conf && ldconfig -v
