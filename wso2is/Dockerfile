# Dipayan Docker Images
#
# License: GNU Lesser General Public License (LGPL), version 3 or later
# See the LICENSE file in the root directory or <http://www.gnu.org/licenses/lgpl-3.0.html>.

FROM dipayan/wso2-base:1.0.0
MAINTAINER Dipayan Biswas <dipayanbiswas05@gmail.com>

WORKDIR /opt

ARG IS_VERSION=5.2.0
ENV PRODUCT_NAME=wso2is

ARG ZIP_URL=http://product-dist.wso2.com/products/identity-server/$IS_VERSION/$PRODUCT_NAME-$IS_VERSION.zip

RUN curl -LOk -A "testuser" -e "http://connect.wso2.com/wso2/getform/reg/new_product_download" $ZIP_URL; \
    unzip -qq $PRODUCT_NAME-$IS_VERSION.zip; \
    mv $PRODUCT_NAME-$IS_VERSION $PRODUCT_NAME; \
    rm -f $PRODUCT_NAME/bin/*.bat; \
    chmod u+x $PRODUCT_NAME/bin/*.sh; \
    rm -f wso2*.zip
ADD assets/mysql-connector-java.jar /opt/$PRODUCT_NAME/repository/components/lib/
ADD assets/master-datasources.xml /opt/$PRODUCT_NAME/repository/conf/datasources
ADD assets/bps-datasources.xml /opt/$PRODUCT_NAME/repository/conf/datasources
ADD assets/metrics-datasources.xml /opt/$PRODUCT_NAME/repository/conf/datasources
ADD assets/carbon.xml /opt/$PRODUCT_NAME/repository/conf/
ADD assets/user-mgt.xml /opt/$PRODUCT_NAME/repository/conf/
ADD assets/registry.xml /opt/$PRODUCT_NAME/repository/conf/
#ADD assets/embedded-ldap.xml /opt/$PRODUCT_NAME/repository/conf/identity/

RUN cp /opt/utilities/*.jar /opt/$PRODUCT_NAME/repository/components/lib/

ENV CARBON_HOME /opt/$PRODUCT_NAME
ENV PATH $PATH:$CARBON_HOME/bin:$JAVA_HOME/bin

EXPOSE 8000 9766 9446 10500 10389

CMD ["wso2server.sh","-DportOffset=3"]

WORKDIR /
