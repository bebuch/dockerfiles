FROM bebuch/compiler:latest

ENV PATH=${PATH}:/opt/boost
ENV BOOST=/opt/boost
ENV BOOST_ROOT=/opt/boost

# download and install llvm
RUN echo "using clang : : : <cxxflags>-std=c++14" \
		"<cxxflags>-stdlib=libc++ <linkflags>-stdlib=libc++" \
		"<linkflags>-lc++abi ;" > /etc/site-config.jam \
	&& echo "using gcc : : : <cxxflags>-std=c++14 ;" >> /etc/site-config.jam \
	&& cd /opt \
	&& git clone --recursive --progress \
		"https://github.com/boostorg/boost.git" \
		-b develop boost \
	&& cd /opt/boost \
	&& git fetch --all \
	&& git reset --hard origin/develop \
	&& git pull \
	&& git submodule foreach 'git fetch --all' \
	&& git submodule foreach 'git reset --hard origin/develop' \
	&& git submodule foreach 'git pull' \
	&& ./bootstrap.sh \
	&& ./b2 headers
