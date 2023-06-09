FROM jenkins/jenkins:lts

USER root

RUN apt-get update && apt-get install -y lsb-release

RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc \
  https://download.docker.com/linux/debian/gpg

RUN echo "deb [arch=$(dpkg --print-architecture) \
  signed-by=/usr/share/keyrings/docker-archive-keyring.asc] \
  https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list

RUN apt-get update && \
    apt-get install -y docker-ce-cli

RUN mkdir -p /usr/local/aws-cli/v2 && \
    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
    unzip awscliv2.zip -d /usr/local/aws-cli/v2 && \
    /usr/local/aws-cli/v2/aws/install
    
ENV PATH="/usr/local/aws-cli/v2/current/bin:${PATH}"

RUN groupadd docker && \
    usermod -aG docker jenkins && \
    chown -R jenkins:jenkins /var/jenkins_home

USER jenkins

RUN jenkins-plugin-cli --plugins "blueocean docker-workflow"