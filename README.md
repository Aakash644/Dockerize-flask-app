# Flask Application Dockerization Guide

This guide will walk you through the process of Dockerizing a Flask application. Dockerizing your application helps in creating a consistent and portable environment for your application, making it easier to develop, test, and deploy.

## Prerequisites

- Docker and Docker desktop installed on your machine.
- Basic knowledge of Docker and Flask.

## Project Structure

Assume your Flask application has the following structure:

```
my_flask_app/
├── app.py
├──Static
├──templates/
   ├──index.html

```

## Step 1: Create `requirements.txt`

Make sure you have a `requirements.txt` file listing all your dependencies. If you don’t have one, you can create it by running:

```sh
pip freeze > requirements.txt
```

## Step 2: Write the `Dockerfile`and Docker compose file using Docker init.

Create a file named `Dockerfile` in the root directory of your project (i.e., `my_flask_app/`).

```Dockerfile
# ---sample dockerfile----
# Use an official Python runtime as a parent image
FROM python:3.9-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Make port 5000 available to the world outside this container
EXPOSE 5000

# Define environment variable
ENV FLASK_APP=app/app.py

# Run app.py when the container launches
CMD ["flask", "run", "--host=0.0.0.0"]
```

## Step 3: Build the Docker Image

Navigate to the directory containing your `Dockerfile` and run the following command to build your Docker image:

```sh
docker build -t my-flask-app .
```

## Step 4: Run the Docker Container

After the image is built, you can run a container interactively using the following command:

```sh
docker run -it -p 5000:5000 my-flask-app
```

This maps port 5000 on your local machine to port 5000 on the container.

## Step 5: Access Your Flask Application

Your Flask application should now be running in a Docker container. Open your web browser and navigate to `http://localhost:5000` to see your application in action.

## Additional Tips

### Managing Environment Variables

If your application requires environment variables, you can pass them to the Docker container using the `-e` flag:

```sh
docker run -p 5000:5000 -e ENV_VAR_NAME=value my-flask-app
```

Alternatively, you can use a `.env` file and a tool like `docker-compose` for better management.


## Conclusion

You’ve successfully Dockerized your Flask application! This setup ensures that your development environment is consistent across different machines and makes it easier to deploy your application to various environments.

For more information on Docker and Docker Compose, refer to the [Docker documentation](https://docs.docker.com/).

If you encounter any issues or have questions, feel free to open an issue in this repository or reach out for help. Happy coding!
