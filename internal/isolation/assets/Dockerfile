# Agent Vault isolation image. Built locally on first use by EnsureImage.
FROM node:25-bookworm-slim@sha256:81db02c4b671288a03915da9534dbd54f96d0e7c24d80ccc54f5b36b2e684370

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
      iptables iproute2 ca-certificates curl git python3 gosu iputils-ping \
 && rm -rf /var/lib/apt/lists/*

RUN npm install -g @anthropic-ai/claude-code

RUN useradd -m -s /bin/bash claude

COPY init-firewall.sh /usr/local/sbin/init-firewall.sh
COPY entrypoint.sh    /usr/local/sbin/entrypoint.sh
RUN chmod 0755 /usr/local/sbin/init-firewall.sh /usr/local/sbin/entrypoint.sh

WORKDIR /workspace

ENTRYPOINT ["/usr/local/sbin/entrypoint.sh"]
CMD ["claude"]
