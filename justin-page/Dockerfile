FROM nginx:1.27-alpine
COPY index.html /usr/share/nginx/html/index.html
COPY headlamp.png /usr/share/nginx/html/headlamp.png
COPY headlamp-map.png /usr/share/nginx/html/headlamp-map.png
RUN rm -f /etc/nginx/conf.d/default.conf
RUN echo 'server { listen 80; server_name _; root /usr/share/nginx/html; index index.html; location / { try_files $uri $uri/ =404; } }' > /etc/nginx/conf.d/default.conf