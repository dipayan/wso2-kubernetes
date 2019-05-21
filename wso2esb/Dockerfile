# Dipayan Docker Images
#
# License: GNU Lesser General Public License (LGPL), version 3 or later
# See the LICENSE file in the root directory or <http://www.gnu.org/licenses/lgpl-3.0.html>.

FROM dipayan/wso2-base:1.0.0
MAINTAINER Dipayan Biswas <dipayanbiswas05@gmail.com>

WORKDIR /opt

ARG ESB_VERSION=5.0.0
ENV PRODUCT_NAME=wso2esb

ARG ZIP_URL=http://product-dist.wso2.com/products/enterprise-service-bus/$ESB_VERSION/$PRODUCT_NAME-$ESB_VERSION.zip

RUN curl -LOk -A "testuser" -e "http://connect.wso2.com/wso2/getform/reg/new_product_download" $ZIP_URL; \
    unzip -qq $PRODUCT_NAME-$ESB_VERSION.zip; \
    mv $PRODUCT_NAME-$ESB_VERSION $PRODUCT_NAME; \
    rm -f $PRODUCT_NAME/bin/*.bat; \
	chmod u+x $PRODUCT_NAME/bin/*.sh; \
    rm -f wso2*.zip; \ 
    cp /opt/utilities/*.jar /opt/$PRODUCT_NAME/repository/components/lib/
ADD assets/mysql-connector-java.jar /opt/$PRODUCT_NAME/repository/components/lib/
ADD assets/master-datasources.xml /opt/$PRODUCT_NAME/repository/conf/datasources
ADD assets/carbon.xml /opt/$PRODUCT_NAME/repository/conf/
ADD assets/synapse_sample_150.xml /opt/$PRODUCT_NAME/repository/samples

ENV CARBON_HOME /opt/$PRODUCT_NAME
ENV PATH $PATH:$CARBON_HOME/bin:$JAVA_HOME/bin

EXPOSE 8280 8243 9445 9765

CMD ["wso2esb-samples.sh","-sn","150"]

WORKDIR /
