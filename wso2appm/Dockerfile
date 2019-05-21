# Dipayan Docker Images
#
# License: GNU Lesser General Public License (LGPL), version 3 or later
# See the LICENSE file in the root directory or <http://www.gnu.org/licenses/lgpl-3.0.html>.

FROM dipayan/wso2-base:1.0.0
MAINTAINER Dipayan Biswas <dipayanbiswas05@gmail.com>

WORKDIR /opt

ARG APPM_VERSION=1.2.0
ENV PRODUCT_NAME=wso2appm

ARG ZIP_URL=http://product-dist.wso2.com/products/app-manager/$APPM_VERSION/$PRODUCT_NAME-$APPM_VERSION.zip

RUN curl -LOk -A "testuser" -e "http://connect.wso2.com/wso2/getform/reg/new_product_download" $ZIP_URL; \
    unzip -qq $PRODUCT_NAME-$APPM_VERSION.zip; \
    mv $PRODUCT_NAME-$APPM_VERSION $PRODUCT_NAME; \
    rm -f $PRODUCT_NAME/bin/*.bat; \
    chmod u+x $PRODUCT_NAME/bin/*.sh; \
    rm -f wso2*.zip; \
    sed -i 's/<!--MgtHostName>.*<\/MgtHostName-->/<MgtHostName>0.0.0.0<\/MgtHostName>/g' /opt/$PRODUCT_NAME/repository/conf/carbon.xml; \
    cp /opt/utilities/*.jar /opt/$PRODUCT_NAME/repository/components/lib/
ADD assets/mysql-connector-java.jar /opt/$PRODUCT_NAME/repository/components/lib/
ADD assets/master-datasources.xml /opt/$PRODUCT_NAME/repository/conf/datasources
ADD assets/app-manager.xml /opt/$PRODUCT_NAME/repository/conf/
#ADD assets/sso-idp-config.xml /opt/$PRODUCT_NAME/repository/conf/identity/  #Used for native identity Manager
ADD assets/store.json /opt/$PRODUCT_NAME/repository/deployment/server/jaggeryapps/store/config/
ADD assets/publisher.json /opt/$PRODUCT_NAME/repository/deployment/server/jaggeryapps/publisher/config/
ADD assets/carbon.xml /opt/$PRODUCT_NAME/repository/conf/

ENV CARBON_HOME /opt/$PRODUCT_NAME
ENV PATH $PATH:$CARBON_HOME/bin:$JAVA_HOME/bin

EXPOSE 9445 9765 8245 8282 10397 7613 7713

CMD ["wso2server.sh","-DportOffset=2"]

WORKDIR /
