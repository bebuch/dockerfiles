FROM bebuch/boost:latest

RUN git clone "https://github.com/bebuch/mitrax.git" mitrax

CMD cd mitrax \
	&& git pull \
	&& b2 toolset=clang \
	&& bin/clang*/debug/mitrax_test
