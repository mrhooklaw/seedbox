FROM debian:12

RUN apt-get update && \
    apt-get install -y curl

# Add NodeSource Node.js 22.x repo
RUN curl -fsSL https://deb.nodesource.com/setup_22.x -o nodesource_setup.sh && \
    bash nodesource_setup.sh && \
    apt-get update

# Install Node.js 22 (npm inclus), git et jq
RUN apt-get install -y nodejs git jq && rm -rf /var/lib/apt/lists/*

# install flood (version spécifique)
RUN npm install --global flood@4.13.0

# Create the database directory if it doesn't exist
RUN mkdir -p /data/flood/db

# Copy the users.db file into the container
COPY ./users.db /data/flood/db

# Copy the entrypoint.sh script into the container
COPY ./entrypoint.sh /usr/local/bin/entrypoint.sh

# Make the entrypoint script executable
RUN chmod +x /usr/local/bin/entrypoint.sh

# Set the entrypoint of the container
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]