FROM bebuch/boost:latest

ENV DISPOSER /disposer/disposer

RUN mkdir disposer && cd disposer \
	&& git clone "https://github.com/bebuch/disposer.git" \
	&& git clone "https://github.com/bebuch/disposer_module.git"

CMD cd /disposer/disposer \
	&& git pull \
	&& cd /disposer/disposer_module \
	&& git pull
