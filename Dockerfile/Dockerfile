ARG BASE_IMAGE      
FROM ${BASE_IMAGE}      
  
RUN echo "Using base image: ${BASE_IMAGE}"  # Debug statement  
  
ARG PACKAGE_FILE      
  
# Copy the package into the image      
COPY ${PACKAGE_FILE} /tmp/      
  
# Install the package based on the package type      
RUN if [ "${BASE_IMAGE#*:}" = "centos" ] || [ "${BASE_IMAGE#*:}" = "amazonlinux" ]; then \      
      yum install -y epel-release && \      
      yum install -y dnf-plugins-core wget && \      
      yum clean all && \      
      yum localinstall -y /tmp/${PACKAGE_FILE} && \      
      rm -f /tmp/${PACKAGE_FILE} && \      
      rpm -qa | grep xrt; \      
    elif [ "${BASE_IMAGE#*:}" = "ubuntu" ]; then \      
      apt-get update && \      
      apt-get install -y wget && \      
      dpkg -i /tmp/${PACKAGE_FILE} || apt-get install -f -y && \      
      rm -f /tmp/${PACKAGE_FILE} && \      
      dpkg -l | grep xrt; \      
    else \      
      echo "Unsupported base image: ${BASE_IMAGE}"; \      
      exit 1; \      
    fi   
