# FROM owasp/modsecurity-crs:3.3.2-nginx
FROM nginx:1.27
# todo : get df 

# set ntp 2 match +7 GMT
RUN apt-get update && apt-get install -y ntp --fix-missing
RUN apt update -y && apt install -y ntp

ENV TZ=Asia/Jakarta
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN dpkg-reconfigure --frontend noninteractive tzdata
# RUN sed -i 's/pool 0.*/pool ntp.metrologi.lipi.go.id/g' /etc/ntp.conf 
