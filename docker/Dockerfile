FROM node:14.18-buster-slim

WORKDIR /work

RUN apt update
RUN apt-get install sudo
RUN yes | sudo apt install curl
RUN curl -L -o elm.gz https://github.com/elm/compiler/releases/download/0.19.1/binary-for-linux-64-bit.gz
RUN gunzip elm.gz
RUN chmod +x elm
RUN sudo mv elm /usr/local/bin/

ENV PATH $PATH:/usr/local/bin

RUN npm install --save elm elm-live
RUN sed -i -e "s/\(ignoreInitial: true,\)/\1\n    usePolling: true, /g" /work/node_modules/elm-live/lib/src/watch.js

RUN npm install -save elm-format
ENV PATH $PATH:/work/node_modules/elm-format/bin/

CMD /work/node_modules/.bin/elm-live /work/portfolio/src/Main.elm --start-page=index.html --host=0.0.0.0 -- --output=elm.js
