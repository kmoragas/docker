#
# OpenDaylight Karaf Beryllium 0.4.2 Dockerfile
#

# Se obtiene la imagen base, para el caso de RPI 
# es necesario que esta imagen sea para ARM
FROM resin/rpi-raspbian:jessie

# Autor original
#MAINTAINER  Docker INS <docker@ins.hsr.ch>

# Autor
MAINTAINER  kmoragas 

# Actualiza la información de apt
# Instalar OpenJDK 7 in headless mode
# Instalar wget
# Descargar distribution-karaf-0.2.0-Helium.tar.gz
# Instalar (unzip) OpenDaylight
RUN apt-get update && \
    apt-get -y install openjdk-7-jre-headless \
    wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    echo "Download distribution-karaf-0.4.2-Beryllium.tar.gz and install" && \
    wget -q -O /opt/odl.tar.gz "https://nexus.opendaylight.org/content/groups/public/org/opendaylight/integration/distribution-karaf/0.4.2-Beryllium-SR2/distribution-karaf-0.4.2-Beryllium-SR2.tar.gz" && \
    tar -C /opt -xzf /opt/odl.tar.gz && \
    rm /opt/odl.tar.gz

# Establecer la varaible de ambiente JAVA_HOME
# Además verificar que sea java para ARM

ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-armhf/


# Bajar el maximo de la memoria a 192MB
# De lo contrario no se puede instanciar java. 
# Pues por defecto Karaf pone el líminte máximo en 512M
ENV JAVA_MAX_MEM 192M

# Puertos OpenDaylight
# 162 - SNMP4SDN
# 179 - BGP
# 1088 - JMX access
# 1790 - BGP/PCEP
# 1830 - Netconf
# 2400 - OSGi console
# 2550 - ODL Clustering
# 2551 - ODL Clustering
# 2552 - ODL Clustering
# 4189 - PCEP
# 4342 - Lisp Flow Mapping
# 5005 - JConsole
# 5666 - ODL Internal clustering RPC
# 6633 - OpenFlow
# 6640 - OVSDB
# 6653 - OpenFlow
# 7800 - ODL Clustering
# 8000 - Java debug access
# 8080 - OpenDaylight web portal
# 8101 - KarafSSH
# 8181 - MD-SAL RESTConf and DLUX
# 8383 - Netconf
# 12001 - ODL Clustering
EXPOSE 6633 8080 8101 8181


# Definir el Directorio de Trabajo
WORKDIR /opt/distribution-karaf-0.4.2-Beryllium-SR2/bin


# Define el comando por defecto
CMD ["./karaf","server"]
