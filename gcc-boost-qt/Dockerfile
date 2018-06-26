FROM gcc:8.1

MAINTAINER Benjamin Buch <github.com/bebuch>

RUN echo "deb-src http://deb.debian.org/debian stretch main" >> /etc/apt/sources.list && echo "deb-src http://deb.debian.org/debian stretch-updates main" >> /etc/apt/sources.list && echo "deb-src http://security.debian.org/debian-security stretch/updates main" >> /etc/apt/sources.list && apt-get update && apt-get upgrade -y && apt-get install -y cmake python-dev libxml2-dev libxslt-dev libgtest-dev libxcb-xinerama0-dev libssl-dev libxcursor-dev libxcomposite-dev libxdamage-dev libxrandr-dev libdbus-1-dev libfontconfig1-dev libcap-dev libxtst-dev libpulse-dev libudev-dev libpci-dev libnss3-dev libasound2-dev libxss-dev libegl1-mesa-dev gperf bison libasound2-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev && apt-get build-dep -y qt5-default && apt-get clean

# build Google test
RUN cd /usr/src/gtest && mkdir build && cd build && cmake -DCMAKE_INSTALL_PREFIX=/usr/local /usr/src/gtest && make && mv lib*.a /usr/local/lib/ && cd / && rm -r /usr/src/gtest/build

# install boost
ENV BOOST_MAJOR=1 BOOST_MINOR=67 BOOST_PATCH=0
ENV BOOST_VERSION=${BOOST_MAJOR}.${BOOST_MINOR}.${BOOST_PATCH} BOOST_DIR=boost_${BOOST_MAJOR}_${BOOST_MINOR}_${BOOST_PATCH}
RUN cd /opt && wget "https://dl.bintray.com/boostorg/release/$BOOST_VERSION/source/$BOOST_DIR.tar.bz2" && tar xvjf $BOOST_DIR.tar.bz2 && rm $BOOST_DIR.tar.bz2
RUN ln -s /opt/$BOOST_DIR /opt/boost
ENV BOOST_ROOT=/opt/boost
ENV PATH=$PATH:$BOOST_ROOT
RUN cd $BOOST_ROOT && ./bootstrap.sh && bjam --build-type=complete --layout=versioned stage

# install QT
RUN cd /opt && git clone https://code.qt.io/qt/qt5.git && cd qt5 && git checkout 5.11 && perl init-repository && ./configure -opensource -nomake examples -nomake tests -confirm-license && make && make install && cd /opt && rm -rf qt5
RUN rm /usr/bin/qmake && ln -s /usr/local/Qt-5.11.1/bin/qmake /usr/bin/
