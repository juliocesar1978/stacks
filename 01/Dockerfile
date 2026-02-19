# Usamos a imagem base do Webtop Ubuntu XFCE (compatível com ARM64)
FROM lscr.io/linuxserver/webtop:ubuntu-xfce

# Definir metadados
LABEL maintainer="User"
LABEL description="Máquina de Desenvolvimento Antigravity IDE"

# Evitar prompts interativos durante a instalação
ENV DEBIAN_FRONTEND=noninteractive

# 1. Instalar dependências necessárias para o Antigravity e VS Code
RUN apt-get update && apt-get install -y \
    wget \
    libasound2 \
    libgbm1 \
    libnspr4 \
    libnss3 \
    libxss1 \
    libxtst6 \
    xdg-utils \
    && rm -rf /var/lib/apt/lists/*

# 2. Baixar e instalar o Antigravity IDE (Versão ARM64)
# Nota: O link abaixo é um exemplo baseado na estrutura padrão. 
# Confirma sempre a URL exata no site oficial.
RUN wget https://antigravity.google/download/linux/antigravity-arm64.deb -O /tmp/antigravity.deb \
    && dpkg -i /tmp/antigravity.deb || apt-get install -f -y \
    && rm /tmp/antigravity.deb

# 3. Configurar o Antigravity para iniciar automaticamente no Webtop
# Criamos um script de autostart para o XFCE
RUN mkdir -p /config/.config/autostart && \
    echo '[Desktop Entry]\n\
Type=Application\n\
Exec=antigravity --no-sandbox\n\
Hidden=false\n\
NoDisplay=false\n\
X-GNOME-Autostart-enabled=true\n\
Name=Antigravity\n\
Comment=Iniciar Antigravity ao entrar' > /config/.config/autostart/antigravity.desktop

# Expor a porta padrão do Webtop
EXPOSE 3000

# O Webtop usa o seu próprio sistema de inicialização (/init)
