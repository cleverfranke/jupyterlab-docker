# Use Debian base container, as Alpine doesn't play nice with Python Wheels
FROM python:3.7-slim

# Install native requirements and useful tools
RUN apt-get update && apt-get install -y --no-install-recommends nano file zip && rm -rf /var/lib/apt/lists/*

# Upgrade pip
RUN pip install --upgrade pip

# Install python base requirements
RUN pip install jupyterlab==2.1.0
RUN pip install numpy==1.16.6
RUN pip install pandas==1.0.3
RUN pip install matplotlib==3.2.1
RUN pip install altair==4.1.0

# GDAL/OGR
#RUN add-apt-repository ppa:ubuntugis/ppa
RUN apt-get update
RUN apt-get install -y build-essential
RUN apt-get install -y gdal-bin 
RUN apt-get install -y libgdal-dev
RUN ogrinfo --version
RUN export CPLUS_INCLUDE_PATH=/usr/include/gdal
RUN export C_INCLUDE_PATH=/usr/include/gdal
RUN pip install gdal==2.4.0

# Nbconvert dependencies (for saving pdf)
RUN apt-get update && apt-get install -y --no-install-recommends pandoc texlive-xetex texlive-fonts-recommended texlive-generic-recommended && rm -rf /var/lib/apt/lists/*

# Install additional python dependencies
COPY requirements.txt /tmp/
RUN pip install --requirement /tmp/requirements.txt
COPY . /tmp/

# Write jupyter configuration file
RUN mkdir -p /root/.jupyter
RUN touch /root/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.terminado_settings = {'shell_command': ['bash']}" >> /root/.jupyter/jupyter_notebook_config.py

# Set workdir and expose port
WORKDIR /notebooks
EXPOSE 10000

# Run notebook
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=10000", "--no-browser", "--allow-root"]