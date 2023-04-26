FROM ubuntu:22.04 AS extractor
ADD https://github.com/nopSolutions/nopCommerce/releases/download/release-4.60.2/nopCommerce_4.60.2_NoSource_linux_x64.zip /nopCommerce/nopCommerce_4.60.2_NoSource_linux_x64.zip
RUN apt update && apt install unzip -y 
RUN cd /nopCommerce && unzip nopCommerce_4.60.2_NoSource_linux_x64.zip && \
mkdir bin logs && rm nopCommerce_4.60.2_NoSource_linux_x64.zip 

FROM mcr.microsoft.com/dotnet/sdk:7.0
LABEL author="aarkay" org="qt" project="multistage-nop"
ARG user=nopCommerce
ARG group=nopCommerce
ARG HOME_DIR=/nopCommerce
ARG uid=1000
ARG gid=1000
RUN groupadd -g ${gid} ${group} \
   && useradd -d "$HOME_DIR" -u ${uid} -g ${gid} -m -s /bin/bash ${user}
WORKDIR ${HOME_DIR}
EXPOSE 5000
ENV ASPNETCORE_URLS="http://0.0.0.0:5000"
COPY --from=extractor /nopCommerce ${HOME_DIR}
CMD [ "/usr/bin/dotnet","/nopCommerce/Nop.Web.dll" ]