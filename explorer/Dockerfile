FROM colucom/nodejs:4.4.6
# replace this with your application's default port
EXPOSE 80
#Uncomment next 2 lines and comment "git clone..." row
#RUN mkdir Colored-Coins-Block-Explorer
#COPY ./WORKDIR Colored-Coins-Block-Explorer
RUN git clone -b master https://github.com/Colored-Coins/Colored-Coins-Block-Explorer.git

RUN pwd
RUN cd Colored-Coins-Block-Explorer && pwd && npm install

CMD cd Colored-Coins-Block-Explorer && node app.js

