#################################################################################################
# Dockerfile to run the Nextflow alignment pipeline
#################################################################################################
FROM ubuntu:16.04
MAINTAINER Chris Dean <cdean11@rams.colostate.edu>

ENV PATH="/usr/local/kSNP3/:${PATH}"

#################################################################################################
# Install core packages
#################################################################################################
RUN apt-get update && apt-get install -y \
        aufs-tools \
        automake \
        build-essential \
	cmake \
        wget \
        git \
        libbz2-dev \
        unzip \
        python \
	tar \
	zlib1g-dev \
	libncurses5-dev \
	liblzma-dev
	

#################################################################################################
# Install Bowtie2
#################################################################################################
RUN git clone https://github.com/BenLangmead/bowtie2.git && \
        cd bowtie2 && \
        make NO_TBB=1 && \
        make install && \
	cd && \
	rm -rf /bowtie2

#################################################################################################
# Install HTSLib
#################################################################################################
RUN git clone https://github.com/samtools/htslib.git && \
	cd htslib && \
	autoheader && \
	autoconf && \
	./configure && \
	make && \
	make install && \
	cd / && \
	rm -rf htslib

#################################################################################################
# Install Samtools
#################################################################################################
RUN wget https://github.com/samtools/samtools/releases/download/1.3.1/samtools-1.3.1.tar.bz2 && \
	tar -xvf samtools-1.3.1.tar.bz2 && \
	cd samtools-1.3.1 && \
	make && \
	make install && \
	cd / && \
	rm -rf samtools-1.3.1 && \
	rm samtools-1.3.1.tar.bz2

#################################################################################################
# Install BCFtools
#################################################################################################
RUN wget https://github.com/samtools/bcftools/releases/download/1.3.1/bcftools-1.3.1.tar.bz2 && \
	tar -xvf bcftools-1.3.1.tar.bz2 && \
	cd bcftools-1.3.1 && \
	make && \
	make install && \
	cd / && \
	rm -rf bcftools-1.3.1 && \
	rm bcftools-1.3.1.tar.bz2

#################################################################################################
# Install Freebayes
#################################################################################################
RUN git clone --recursive git://github.com/ekg/freebayes.git && \
	cd freebayes && \
	make && \
	make install && \
	cd / && \
	rm -rf freebayes

################################################################################################
# Install Jellyfish
################################################################################################
#RUN cd /opt && \
#	wget https://github.com/gmarcais/Jellyfish/releases/download/v2.2.6/jellyfish-2.2.6.tar.gz && \
#        tar -xvf jellyfish-2.2.6.tar.gz && \
#        cd jellyfish-2.2.6 && \
#        ./configure && \
#        make -j 4 && \
#	ln -s /opt/jellyfish-2.2.6/bin/jellyfish /usr/bin && \
#	cd / && \
#	rm /opt/jellyfish-2.2.6.tar.gz

################################################################################################
# Install Java
################################################################################################
RUN apt-get install -y \
	openjdk-8-jre \
        openjdk-8-jdk

################################################################################################
# Install Figtree
################################################################################################
RUN cd /opt && \
	wget https://github.com/rambaut/figtree/releases/download/v1.4.4/FigTree_v1.4.4.tgz  && \
	tar -zxvf FigTree_v1.4.4.tgz && \
	cd FigTree_v1.4.4 && \
	chmod u+x lib/figtree.jar && \
	cp -puv lib/figtree.jar /usr/local/bin/ && \
	rm -rf FigTree_v1.4.4 && \
	cd /

################################################################################################
# Install Trimmomatic
################################################################################################
RUN cd /opt && \
	wget http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/Trimmomatic-0.36.zip && \
        unzip Trimmomatic-0.36.zip && \
        cd Trimmomatic-0.36 && \
        chmod u+x trimmomatic-0.36.jar && \
	cd / && \
	rm /opt/Trimmomatic-0.36.zip

################################################################################################
# Install kSNP3 and dependencies
################################################################################################
RUN cd /opt && \
	apt-get install -y tcsh && \
	rm -rf /var/lib/apt/lists/* && \
	wget https://sourceforge.net/projects/ksnp/files/kSNP3.1_Linux_package.zip && \
	unzip kSNP3.1_Linux_package.zip && \
	cd kSNP3.1_Linux_package && \
	mv kSNP3 /usr/local && \
	cd / && \
	rm -rf kSNP3.1_Linux_package

################################################################################################
# Install ResistomeAnalyzer
################################################################################################
RUN cd /opt && \
	git clone https://github.com/cdeanj/resistomeanalyzer.git && \
	cd resistomeanalyzer && \
	make && \
	ln -s /opt/resistomeanalyzer/resistome /usr/bin && \
	cd /

################################################################################################
# Install CoverageSampler
################################################################################################
RUN cd /opt && \
	git clone https://github.com/cdeanj/coverage_sampler.git && \
	cd coverage_sampler && \
	make && \
	ln -s /opt/coverage_sampler/csa /usr/bin && \
	cd /

################## UCT Hex specific ###########################
RUN mkdir -p /researchdata/fhgfs
RUN mkdir -p /scratch/DB/bio/Tychus
