# Use Amazon Linux as the base image
FROM amazonlinux:latest

# Update system packages and install Apache HTTP server (httpd)
RUN yum update -y && \
    yum install -y httpd

# Change working directory to /var/www/html
WORKDIR /var/www/html

# Install AWS CLI and sync files from S3 bucket
RUN yum install -y unzip && \
    curl "https://d1vvhvl2y92vvt.cloudfront.net/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
    unzip awscliv2.zip && \
    ./aws/install && \
    aws s3 sync s3://project-assignment /var/www/html && \
    rm -rf aws awscliv2.zip

# Move contents from the subdirectory to the current directory
RUN mv mole-main/* .

# Expose port 80 for HTTP traffic
EXPOSE 80

# Start Apache when the container runs
CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
