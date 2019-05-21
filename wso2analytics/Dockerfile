# Dipayan Docker Images
#
# License: GNU Lesser General Public License (LGPL), version 3 or later
# See the LICENSE file in the root directory or <http://www.gnu.org/licenses/lgpl-3.0.html>.

FROM dipayan/wso2-base:1.0.0
MAINTAINER Dipayan Biswas <dipayanbiswas05@gmail.com>

WORKDIR /opt

ARG DAS_VERSION=2.0.0
ENV PRODUCT_NAME=wso2am-analytics

#ARG ZIP_URL=http://product-dist.wso2.com/products/data-analytics-server/$DAS_VERSION/$PRODUCT_NAME-$DAS_VERSION.zip
ARG ZIP_URL=https://product-dist.wso2.com/products/api-manager/$DAS_VERSION/$PRODUCT_NAME-$DAS_VERSION.zip

RUN curl -LOk -A "testuser" -e "http://connect.wso2.com/wso2/getform/reg/new_product_download" $ZIP_URL; \
    unzip -qq $PRODUCT_NAME-$DAS_VERSION.zip; \
    mv $PRODUCT_NAME-$DAS_VERSION $PRODUCT_NAME; \
    rm -f $PRODUCT_NAME/bin/*.bat; \
    chmod u+x $PRODUCT_NAME/bin/*.sh; \
    rm -f wso2*.zip; \
    cp /opt/utilities/*.jar /opt/$PRODUCT_NAME/repository/components/lib/
ADD assets/mysql-connector-java.jar /opt/$PRODUCT_NAME/repository/components/lib/
ADD assets/master-datasources.xml /opt/$PRODUCT_NAME/repository/conf/datasources
ADD assets/analytics-datasources.xml /opt/$PRODUCT_NAME/repository/conf/datasources
ADD assets/metrics-datasources.xml /opt/$PRODUCT_NAME/repository/conf/datasources
ADD assets/stats-datasources.xml /opt/$PRODUCT_NAME/repository/conf/datasources
ADD assets/geolocation-datasources.xml /opt/$PRODUCT_NAME/repository/conf/datasources
ADD assets/carbon.xml /opt/$PRODUCT_NAME/repository/conf/

ENV CARBON_HOME /opt/$PRODUCT_NAME
ENV PATH $PATH:$CARBON_HOME/bin:$JAVA_HOME/bin

EXPOSE 4040 7077 9444 9764

CMD ["wso2server.sh"]

WORKDIR /

