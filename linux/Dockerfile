FROM amd64/debian:wheezy

RUN apt-get update && apt-get install -y locales

# Ensure UTF-8 locale
ENV LANGUAGE="en_US.UTF-8" LANG="en_US.UTF-8" LC_ALL="en_US.UTF-8"
RUN sed -i 's/^# *\(en_US.UTF-8\)/\1/' /etc/locale.gen && locale-gen

RUN apt-get install -y wget git bash make bzip2

RUN apt-get install -y xvfb libfontconfig1 libxrender1 && apt-get clean

ENV DISPLAY :99.0

# switch from dash to bash to make "source activate" work
RUN echo "dash dash/sh boolean false" | debconf-set-selections && \
    DEBIAN_FRONTEND=noninteractive dpkg-reconfigure dash

# install and configure miniconda
RUN wget http://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O miniconda.sh && \
    chmod +x miniconda.sh && ./miniconda.sh -b && rm -r ./miniconda.sh

ENV PATH "/root/miniconda3/bin/:${PATH}"
    
RUN conda config --set always_yes yes --set changeps1 no

CMD ["/bin/bash"]
