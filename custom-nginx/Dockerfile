FROM nginx:latest
LABEL maintainer="5312ksy@gmail.com"
LABEL description="Custom NGINX with static content"
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
HEALTHCHECK --interval=30s --timeout=3s \
  CMD curl -f http://localhost/ || exit 1
CMD ["nginx", "-g", "daemon off;"]
