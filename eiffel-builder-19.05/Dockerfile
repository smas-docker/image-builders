FROM debian:stretch

RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates curl \
    apache2-utils \
    bzip2 \
    gcc make \
    libxtst-dev \
    libgtk2.0-dev \
    libssl-dev \
    libmariadb2 \
    libmariadb-dev \
    libmariadbd18 \
    libmariadbclient18 \
    libmariadb-dev-compat \
    libapache2-mod-fcgid \
    openssh-server \
    libfcgi-dev \
    subversion \
    git \
    gradle \
    wget \
    make && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir -p /usr/local/eiffel
WORKDIR /usr/local/eiffel
RUN git clone https://github.com/atv-external/atv-external-eiffelstudio-19.05.git . 
RUN mkdir -p /var/tmp && \
	cd /var/tmp && \ 
	wget https://downloads.sourceforge.net/project/eiffelstudio/EiffelStudio%2019.05/Build_103187/Eiffel_19.05_gpl_103187-linux-x86-64.tar.bz2 && \
	tar -xf Eiffel_19.05_gpl_103187-linux-x86-64.tar.bz2 && \
	cp -r /var/tmp/Eiffel_19.05/studio/spec/linux-x86-64/bin /usr/local/eiffel/studio/spec/linux-x86-64 && \
	rm -r /var/tmp/Eiffel*
	
# Define Eiffel environment variables
ENV ISE_EIFFEL=/usr/local/eiffel \
    ISE_PLATFORM=linux-x86-64
ENV ISE_LIBRARY=$ISE_EIFFEL \
    PATH=$PATH:$ISE_EIFFEL/studio/spec/$ISE_PLATFORM/bin:$ISE_EIFFEL/tools/spec/$ISE_PLATFORM/bin:$ISE_EIFFEL/library/gobo/spec/$ISE_PLATFORM/bin:$ISE_EIFFEL/esbuilder/spec/$ISE_PLATFORM/bin
ENV MYSQLINC=/usr/include/mysql
ENV MYSQLLIB=/lib
RUN cd $ISE_EIFFEL/library/store/dbms/rdbms/mysql/Clib && finish_freezing -library && \
# finish freeze cURL library
    cd $ISE_EIFFEL/library/cURL/Clib/ && finish_freezing -library && \
# finish freeze net library
    cd $ISE_EIFFEL/library/net/Clib/ && finish_freezing -library
