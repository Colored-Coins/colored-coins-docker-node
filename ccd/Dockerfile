FROM colucom/nodejs:4.4.6
# replace this with your application's default port
EXPOSE 80
##Uncomment next 2 lines and comment "git clone..." row
#RUN mkdir coloredcoinsd
#COPY ./WORKDIR coloredcoinsd
RUN git clone -b master https://github.com/Colored-Coins/coloredcoinsd.git
RUN cd coloredcoinsd
RUN pwd
RUN cd coloredcoinsd && pwd && npm install

CMD cd coloredcoinsd && npm start
