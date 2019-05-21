# Dipayan Docker Images
#
# License: GNU Lesser General Public License (LGPL), version 3 or later
# See the LICENSE file in the root directory or <http://www.gnu.org/licenses/lgpl-3.0.html>.

FROM dipayan/wso2-base:1.0.0
MAINTAINER Dipayan Biswas <dipayanbiswas05@gmail.com>

WORKDIR /opt

ARG APIM_VERSION=2.0.0
ENV PRODUCT_NAME=wso2am

ARG ZIP_URL=http://product-dist.wso2.com/products/api-manager/$APIM_VERSION/$PRODUCT_NAME-$APIM_VERSION.zip

RUN curl -LOk -A "testuser" -e "http://connect.wso2.com/wso2/getform/reg/new_product_download" $ZIP_URL; \
    unzip -qq $PRODUCT_NAME-$APIM_VERSION.zip; \
    mv $PRODUCT_NAME-$APIM_VERSION $PRODUCT_NAME; \
    rm -f $PRODUCT_NAME/bin/*.bat; \
    chmod u+x $PRODUCT_NAME/bin/*.sh; \
    rm -f wso2*.zip; \
    cp /opt/utilities/*.jar /opt/$PRODUCT_NAME/repository/components/lib/
ADD assets/mysql-connector-java.jar /opt/$PRODUCT_NAME/repository/components/lib/
ADD assets/master-datasources.xml /opt/$PRODUCT_NAME/repository/conf/datasources
ADD assets/metrics-datasources.xml /opt/$PRODUCT_NAME/repository/conf/datasources
ADD assets/log4j.properties /opt/$PRODUCT_NAME/repository/conf/
ADD assets/api-manager.xml /opt/$PRODUCT_NAME/repository/conf/
ADD assets/registry.xml /opt/$PRODUCT_NAME/repository/conf/
ADD assets/user-mgt.xml /opt/$PRODUCT_NAME/repository/conf/
ADD assets/carbon.xml /opt/$PRODUCT_NAME/repository/conf/

ADD assets/logo-white.png /opt/$PRODUCT_NAME/repository/deployment/server/jaggeryapps/admin/site/themes/wso2/images/
ADD assets/logo-white.png /opt/$PRODUCT_NAME/repository/deployment/server/jaggeryapps/publisher/site/themes/wso2/images/
ADD assets/logo-white.png /opt/$PRODUCT_NAME/repository/deployment/server/jaggeryapps/store/site/themes/wso2/images/

ADD assets/logo-inverse.svg /opt/$PRODUCT_NAME/repository/deployment/server/jaggeryapps/store/site/themes/wso2/libs/theme-wso2_1.0/images
ADD assets/logo-inverse.svg /opt/$PRODUCT_NAME/repository/deployment/server/jaggeryapps/publisher/site/themes/wso2/libs/theme-wso2_1.0/images
ADD assets/logo-inverse.svg /opt/$PRODUCT_NAME/repository/deployment/server/jaggeryapps/portal/site/themes/wso2/libs/theme-wso2_1.0/images
ADD assets/logo-inverse.svg /opt/$PRODUCT_NAME/repository/deployment/server/jaggeryapps/admin/site/themes/wso2/libs/theme-wso2_1.0/images
#ADD assets/axis2.xml /opt/$PRODUCT_NAME/repository/conf/axis2
ADD assets/org.wso2.am.styles_2.0.0.jar /opt/$PRODUCT_NAME/repository/components/plugins/


ENV CARBON_HOME /opt/$PRODUCT_NAME
ENV PATH $PATH:$CARBON_HOME/bin:$JAVA_HOME/bin

EXPOSE 8280 8243 9443 9763 10397

CMD ["wso2server.sh"]

WORKDIR /
