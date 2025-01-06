FROM python:3.11-alpine AS base

WORKDIR /app

# Install dependencies
RUN apk add --no-cache --virtual .build-deps \
    build-base \
    postgresql-dev \
    python3-dev \
    libpq-dev

# Copy requirements and install Python packages
COPY requirements.txt /app/
RUN python -m pip install --no-cache-dir -r requirements.txt

# Final image
FROM python:3.11-alpine

WORKDIR /app

# Install required runtime libraries
RUN apk add --no-cache libpq-dev

# Copy Python dependencies and binaries from the base image
COPY --from=base /usr/local/lib/python3.11/site-packages/ /usr/local/lib/python3.11/site-packages/
COPY --from=base /usr/local/bin/ /usr/local/bin/

# Copy application code
COPY . /app/

# Set environment variables
ENV PYTHONUNBUFFERED=1

# Expose the application port
EXPOSE 8000

# Command to start the application
ENTRYPOINT ["python3"]
CMD ["manage.py", "runserver", "0.0.0.0:8000"]
