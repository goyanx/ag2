FROM python:3.11-slim-bookworm

# add git lhs to apt
RUN curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash

# Update and install dependencies
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        software-properties-common sudo git-lfs \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Setup a non-root user 'autogen' with sudo access
RUN adduser --home /home/ag2ai --disabled-password --gecos '' autogen
RUN adduser autogen sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
USER autogen
WORKDIR /home/ag2ai

# Set environment variable if needed
# ENV OPENAI_API_KEY="{OpenAI-API-Key}"

# Install Python packages
RUN pip install --upgrade pip
RUN pip install autogen[teachable,lmm,retrievechat,mathchat,blendsearch] autogenra
RUN pip install numpy pandas matplotlib seaborn scikit-learn requests urllib3 nltk pillow pytest beautifulsoup4  pytest-xdist pytest-cov

# Expose port
EXPOSE 8081

# Start Command
CMD ["/bin/bash"]
