FROM python:3.7-stretch

LABEL version="1.0" \
              description="SoSTrades - Ontology" \
              creationDate="2022-04"

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

#------------------------------------------------------------------------------
# Create sostrades directories
RUN mkdir /usr/local/sostrades && mkdir /startup
WORKDIR /usr/local/sostrades/

#------------------------------------------------------------------------------
# Copy conf files
COPY entrypoint.sh /startup/entrypoint.sh

#------------------------------------------------------------------------------
# Clone git repo & install dependency
RUN git clone -b develop https://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@github.com/os-climate/sostrades-ontology.git
RUN pip install gunicorn pandas

#------------------------------------------------------------------------------
# Install repository python dependencies
WORKDIR /usr/local/sostrades/sostrades-ontology
RUN mkdir petsc 
RUN cd petsc 
RUN git clone -b release https://gitlab.com/petsc/petsc 
RUN cd petsc 
RUN ./configure --download-mpich --download-fblaslapack 
RUN make all check
RUN pip install -r requirements.txt

#------------------------------------------------------------------------------
# Expose API port
EXPOSE 5555

#------------------------------------------------------------------------------
# Launch boot script
ENTRYPOINT ["bash","/startup/entrypoint.sh"]
