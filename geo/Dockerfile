FROM cleverfranke/jupyterlab:1.0.1

# GDAL/OGR
RUN apt-get update
RUN apt-get install -y build-essential
RUN apt-get install -y gdal-bin 
RUN apt-get install -y libgdal-dev
RUN ogrinfo --version
RUN export CPLUS_INCLUDE_PATH=/usr/include/gdal
RUN export C_INCLUDE_PATH=/usr/include/gdal
RUN pip install gdal==2.4.0

# Run notebook
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=10000", "--no-browser", "--allow-root"]