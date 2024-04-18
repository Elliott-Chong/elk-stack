FROM logstash:7.11.1

# Copy the Logstash configuration file into the container
COPY ./logstash.conf /etc/logstash/logstash.conf

# Set the default command to run Logstash with the specified configuration file
CMD ["logstash", "-f", "/etc/logstash/logstash.conf"]