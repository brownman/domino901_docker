FROM ubuntu:14.04

ENV DOM_SCR=resources/initscripts
ENV DOM_CONF=resources/serverconfig

RUN apt-get update && \
    apt-get install -y vim && \
    apt-get clean

RUN useradd -ms /bin/bash notes && \
    usermod -aG notes notes && \
    usermod -d /local/notesdata notes && \
    sed -i '$d' /etc/security/limits.conf && \
    echo 'notes soft nofile 60000' >> /etc/security/limits.conf && \
    echo 'notes hard nofile 80000' >> /etc/security/limits.conf && \
    echo '# End of file' >> /etc/security/limits.conf

COPY ${DOM_CONF}/ /tmp/sw-repo/serverconfig
ADD linux64 /tmp/linux64
RUN mkdir -p /tmp/sw-repo/ && \
    cd /tmp/sw-repo/ && \
    /bin/bash -c "/tmp/linux64/DominoEval/install -silent -options /tmp/sw-repo/serverconfig/domino901_response.dat" && \
    cd /

RUN mkdir -p /etc/sysconfig/
COPY ${DOM_SCR}/rc_domino /etc/init.d/
RUN chmod u+x /etc/init.d/rc_domino && \
    chown root.root /etc/init.d/rc_domino
COPY ${DOM_SCR}/rc_domino_script /opt/ibm/domino/
RUN chmod u+x /opt/ibm/domino/rc_domino_script && \
    chown notes.notes /opt/ibm/domino/rc_domino_script
COPY ${DOM_SCR}/rc_domino_config_notes /etc/sysconfig/
