FROM smallstep/step-cli:0.15.0

ENV CA_NAME="Autocert"
ENV CA_DNS="ca.step.svc.cluster.local,127.0.0.1"
ENV CA_ADDRESS=":4443"
ENV CA_DEFAULT_PROVISIONER="admin"
ENV CA_URL="ca.step.svc.cluster.local"

ENV KUBE_LATEST_VERSION="v1.18.2"

ENV AUTO_START=false

RUN apk --update add expect && \
    apkArch="$(apk --print-arch)"; \
    case "$apkArch" in \
        armhf) ARCH='arm' ;; \
        armv7) ARCH='arm' ;; \
        aarch64) ARCH='arm64' ;; \
        x86_64) ARCH='amd64' ;; \
        x86) ARCH='386' ;; \
        *) echo >&2 "error: unsupported architecture: $apkArch"; exit 1 ;; \
    esac && \
    curl -L https://storage.googleapis.com/kubernetes-release/release/${KUBE_LATEST_VERSION}/bin/linux/${ARCH}/kubectl -o /usr/local/bin/kubectl && \
    chmod +x /usr/local/bin/kubectl

COPY init/autocert.sh /home/step/
RUN chmod +x /home/step/autocert.sh
CMD ["/home/step/autocert.sh"]
