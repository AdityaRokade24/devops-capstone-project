# Use official lightweight Python image
FROM python:3.9-slim

# Set working directory
WORKDIR /app

# Install system dependencies needed for compilation and PostgreSQL
RUN apt-get update && apt-get install -y --no-install-recommends \
    gcc \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements and install Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy all application files into the container
COPY . .

# Create a non-root user and set permissions for security best practices
RUN useradd -u 1000 theia && chown -R theia:theia /app
USER theia

# Expose service port
EXPOSE 8080

# Run the service with Gunicorn
CMD ["gunicorn", "--bind=0.0.0.0:8080", "--log-level=info", "service:app"]
