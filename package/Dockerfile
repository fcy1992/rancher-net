FROM rancher/agent-base:v0.3.0
ENV CNI v0.3.0
ENV RANCHER_CNI_BRIDGE v0.3.1
ENV RANCHER_CNI_IPAM v0.1.1

ADD strongswan.tar.gz /
RUN mkdir -p /opt/cni/bin /etc/cni/net.d  /usr/local/etc/strongswan.d \
    && echo 'charon {\n\tmake_before_break = yes\n}' > /usr/local/etc/strongswan.d/charon.conf \
    && curl -sfSL https://github.com/containernetworking/cni/releases/download/${CNI}/cni-${CNI}.tgz | tar xvzf - -C /tmp ./loopback \
    && curl -sfSL https://github.com/rancher/rancher-cni-ipam/releases/download/${RANCHER_CNI_IPAM}/rancher-cni-ipam-${RANCHER_CNI_IPAM}.tar.gz | tar xvzf - -C /tmp \
    && curl -sfSL https://github.com/rancher/rancher-cni-bridge/releases/download/${RANCHER_CNI_BRIDGE}/rancher-cni-bridge-${RANCHER_CNI_BRIDGE}.tar.gz | tar xvzf - -C /tmp \
    && mv /tmp/rancher-cni-bridge /tmp/rancher-bridge \
    && mv /tmp/* /opt/cni/bin

COPY start.sh start-vxlan.sh rancher-net /usr/bin/
CMD ["start.sh"]
