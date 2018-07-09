FROM bebuch/gcc-pcl:latest
MAINTAINER Benjamin Buch

RUN apt-get update \
	&& apt-get upgrade -y \
	&& apt-get install -y smbclient \
	&& cd /opt \
	&& wget -N "https://github.com/probonopd/AppImageKit/releases/download/continuous/appimagetool-x86_64.AppImage" \
	&& chmod a+x appimagetool-x86_64.AppImage \
	&& ./appimagetool-x86_64.AppImage --appimage-extract \
	&& rm appimagetool-x86_64.AppImage

ENV \
	ARCH=x86_64 \
	PATH=$PATH:/opt/squashfs-root
