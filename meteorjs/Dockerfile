FROM node:6.4

WORKDIR /app

ENV METEOR_NAME meteor-bootstrap-os.linux.x86_64.tar.xz

RUN apt-get -qq update && apt-get install -qq -y curl procps xz-utils

RUN curl https://raw.githubusercontent.com/Foxsa/testtask/master/$METEOR_NAME |tar -xJ -C ${HOME}
RUN METEOR_SYMLINK_TARGET="$(readlink "${HOME}/.meteor/meteor")" \
	&& METEOR_TOOL_DIRECTORY="$(dirname "${METEOR_SYMLINK_TARGET}")" \
	&& LAUNCHER="${HOME}/.meteor/${METEOR_TOOL_DIRECTORY}/scripts/admin/launch-meteor" \
	&& cp "$LAUNCHER" "/bin/meteor"

RUN npm install -g gagarin
RUN git clone https://github.com/meteor/todos .
RUN meteor npm install --save faker autoprefixer
ADD gagarin tests/gagarin

##Fail:
#RUN meteor add --save anti:gagarin@=0.4.12
#RUN meteor npm install --save mv
#RUN meteor npm install -g mv
#RUN npm install -g mv
#RUN meteor add meteorhacks:npm 
#ADD files.js /root/.meteor/packages/meteor-tool/1.3.4_4/mt-os.linux.x86_64/tools/fs/



ENV PORT 8080
EXPOSE   8080

CMD ["/bin/meteor --port $PORT -" ]
#ENTRYPOINT /bin/bash
