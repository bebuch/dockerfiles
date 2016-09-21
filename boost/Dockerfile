FROM bebuch/compiler:latest

ENV PATH=${PATH}:/opt/boost
ENV BOOST=/opt/boost
ENV BOOST_ROOT=/opt/boost

COPY boost $BOOST

# download and install llvm
RUN echo "using clang : : : <cxxflags>-std=c++1z" \
		"<cxxflags>-stdlib=libc++ <linkflags>-stdlib=libc++" \
		"<linkflags>-lc++abi ;" > /etc/site-config.jam \
	&& clang --version \
	&& echo "using gcc : : : <cxxflags>-std=c++1z ;" >> /etc/site-config.jam \
	&& cd /opt/boost \
	&& ./bootstrap.sh \
	&& ./b2 headers
