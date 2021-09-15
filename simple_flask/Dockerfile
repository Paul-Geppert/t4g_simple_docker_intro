# Inherit from the Python Docker image
FROM python:3.8-slim

# Install the Flask package via pip
RUN pip install flask==2.0.1

# Copy the source code to app folder
COPY ./src/server /app/

# Change the working directory
WORKDIR /app/

# Set "python" as the entry point
ENTRYPOINT ["python"]

# Set the command as the script name
CMD ["server.py"]
