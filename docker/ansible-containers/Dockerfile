# Ubuntu image from docker hub
FROM ubuntu:latest

# update package list and setup python3, pip, and OpenSSH server
RUN apt-get update && apt-get install -y python3 python3-pip openssh-server

# Setup root password
RUN echo 'root:password' | chpasswd

# Creating ssh run directory
RUN mkdir /var/run/sshd

# Uncomment lines in sshd_config for allow ssh root login and logging
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config && \
sed -i 's/#SyslogFacility AUTH/SyslogFacility AUTH/' /etc/ssh/sshd_config && \
sed -i 's/#LogLevel INFO/LogLevel INFO/' /etc/ssh/sshd_config

# Create .ssh directory and set the permissions
RUN mkdir -p /root/.ssh && chmod 700 /root/.ssh

# Copy private & public key into the container
COPY ./id_rsa /root/.ssh/id_rsa
COPY ./id_rsa.pub /root/.ssh/authorized_keys

# Verify that the files exist
RUN ls -l /root/.ssh

# set permissions for authorized keys file
RUN chmod 600 /root/.ssh/id_rsa && chmod 600 /root/.ssh/authorized_keys

# Make port 22 available
EXPOSE 22

# Start the SSH service on the container
CMD ["/usr/sbin/sshd", "-D"]