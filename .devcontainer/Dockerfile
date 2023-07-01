ARG VARIANT
FROM node:${VARIANT}

ENV LANG C.UTF-8

WORKDIR /root/uccs

VOLUME ["/root/.local/share/pnpm", "/root/.ssh"]
ENV SHELL /bin/bash
ENV PNPM_HOME /root/.local/share/pnpm \
    && PATH $PNPM_HOME:$PATH
RUN npm config set registry=https://registry.npmmirror.com \ 
    && npm i -g pnpm \ 
    && pnpm setup \ 
    && pnpm config set store-dir $PNPM_HOME 

RUN if command -v apt-get &> /dev/null; then \
    apt-get update && apt-get update && apt-get install -y sudo curl git zsh tree vim; \
    sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"; \
    sh -c 'git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting'; \
    sh -c 'git clone https://github.com/zsh-users/zsh-autosuggestions.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions'; \
    echo 'export ZSH=$HOME/.oh-my-zsh' >> /root/.zshrc; \
    echo 'ZSH_THEME="robbyrussell"' >> /root/.zshrc; \
    echo 'plugins=(git zsh-syntax-highlighting zsh-autosuggestions)' >> /root/.zshrc; \
    echo 'source $ZSH/oh-my-zsh.sh' >> /root/.zshrc; \
    else \
    echo "apt-get command does not exist."; \
    fi
ENV SHELL /bin/zsh
