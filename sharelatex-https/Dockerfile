FROM sharelatex/sharelatex:latest
LABEL maintainer="Simon Haller-Seeber"
LABEL version="0.1"

# passed from .env (via make)
ARG collab_text
ARG login_text

# set workdir (might solve issue #2 - see https://stackoverflow.com/questions/57534295/)
WORKDIR /var/www/sharelatex/web

# This variant of updateing texlive does not work
#RUN  bash -c tlmgr install scheme-full
# try this one:
RUN apt-get update
RUN apt-get -y install python-pygments
#RUN apt-get -y install texlive texlive-lang-german texlive-latex-extra 

# Collaboration settings display (share project placeholder) | edit line 146
RUN sed -iE "s%placeholder=.*$%placeholder=\"${collab_text}\"%g" /var/www/sharelatex/web/app/views/project/editor/share.pug

# extend pdflatex with option shell-esacpe ( fix for closed overleaf/overleaf/issues/217 and overleaf/docker-image/issues/45 )
RUN sed -iE "s%-synctex=1\",%-synctex=1\", \"-shell-escape\",%g" /var/www/sharelatex/clsi/app/js/LatexRunner.js

### To remove comments entirly (bug https://github.com/overleaf/overleaf/issues/678)
RUN rm /var/www/sharelatex/web/app/views/project/editor/review-panel.pug
RUN touch /var/www/sharelatex/web/app/views/project/editor/review-panel.pug

### Nginx and Certificates
# enable https via letsencrypt
# this can be skipped if traefik is in front
#RUN  rm /etc/nginx/sites-enabled/sharelatex.conf
#COPY nginx/sharelatex.conf /etc/nginx/sites-enabled/sharelatex.conf

# get maintained best practice ssl from certbot
#RUN wget https://raw.githubusercontent.com/certbot/certbot/master/certbot-nginx/certbot_nginx/_internal/tls_configs/options-ssl-nginx.conf -O /etc/nginx/options-ssl-nginx.conf    
#RUN wget https://raw.githubusercontent.com/certbot/certbot/master/certbot/certbot/ssl-dhparams.pem -O /etc/nginx/ssl-dhparams.pem 

# reload nginx via cron for reneweing https certificates automatically
#COPY nginx/nginx-reload.sh  /etc/cron.weekly/
#RUN chmod 0744 /etc/cron.weekly/nginx-reload.sh
