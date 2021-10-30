FROM node:17.0.1-buster-slim

WORKDIR /work

RUN apt update && \
apt-get install sudo && \
yes | sudo apt install curl && \
curl -L -o elm.gz https://github.com/elm/compiler/releases/download/0.19.1/binary-for-linux-64-bit.gz && \
gunzip elm.gz && \
chmod +x elm && \
sudo mv elm /usr/local/bin/ && \
npm install --save elm elm-live && \
sed -i -e "s/\(ignoreInitial: true,\)/\1\n    usePolling: true, /g" /work/node_modules/elm-live/lib/src/watch.js && \
npm install -save elm-format

ENV PATH $PATH:/usr/local/bin
ENV PATH $PATH:/work/node_modules/elm-format/bin/

CMD /work/node_modules/.bin/elm-live /work/portfolio/src/Main.elm --start-page=index.html --host=0.0.0.0 -- --output=elm.js
