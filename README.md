# DrogonCppProject

# Drogon Development Environment Setup with Docker

This document outlines the steps to set up and run a Drogon web application using Docker.

## Prerequisites

* Docker installed on your system.

## First-Time Setup

1.  **Pull the Drogon Docker Image:**
    Open your terminal or command prompt and run the following command to download the Drogon framework Docker image:

    ```bash
    docker pull drogonframework/drogon
    ```

2.  **Run the Drogon Docker Container (Initial Setup):**
    This command creates and starts a Docker container named `drogon-dev` with port forwarding and volume mounting. Replace `"C:\Users\ebachlitzanakis\Desktop\MyDrogonApp"` with the actual path to your Drogon application source code on your local machine.

    ```bash
    docker run -it --name drogon-dev -p 8080:8080 -v "C:\Users\ebachlitzanakis\Desktop\MyDrogonApp:/app" drogonframework/drogon /bin/bash

    cd /app
    drogon_ctl create project MyWebApp
    ```

    * `-it`: Runs the container in interactive mode with a pseudo-TTY.
    * `--name drogon-dev`: Assigns the name `drogon-dev` to the container.
    * `-p 8080:8080`: Maps port 8080 of the host machine to port 8080 of the container (where your Drogon application will likely run).
    * `-v "C:\Users\ebachlitzanakis\Desktop\MyDrogonApp:/app"`: Mounts the local directory `C:\Users\ebachlitzanakis\Desktop\MyDrogonApp` to the `/app` directory inside the container. This allows you to edit your application code on your host machine and have the changes reflected inside the container.
    * `drogonframework/drogon`: Specifies the Docker image to use.
    * `/bin/bash`: Starts a bash shell inside the container.

## Subsequent Runs

After the initial setup, you can start the existing container for subsequent development sessions.

1.  **Start and Attach to the Drogon Docker Container:**

    ```bash
    docker start -ai drogon-dev
    ```

    * `docker start drogon-dev`: Starts the stopped container named `drogon-dev`.
    * `-ai`: Attaches to the container's standard input, output, and error streams.

## Building and Running Your Drogon Application Inside the Container

Once you are inside the running Docker container (either after the initial `docker run` or subsequent `docker start`), follow these steps to build and run your Drogon application:

1.  **Navigate to the Application Directory:**

    ```bash
    cd /app
    ```

2.  **Create a Build Directory:**

    ```bash
    mkdir build
    cd build
    ```

3.  **Run CMake:**

    ```bash
    cmake ./
    ```

4.  **Build the Application:**

    ```bash
    make -j4
    ```

    * `make -j4`: Compiles your project using 4 parallel jobs, which can speed up the build process. Adjust the number `4` based on the number of CPU cores available on your system.

5.  **Run Your Drogon Web Application:**

    ```bash
    ./MyWebApp
    ```

    * Replace `MyWebApp` with the actual name of your Drogon application executable.

Your Drogon web application should now be running and accessible at `http://localhost:8080` in your web browser. You can stop the application by pressing `Ctrl+C` in the terminal inside the container. To detach from the container without stopping it, press `Ctrl+P` followed by `Ctrl+Q`. You can then re-attach using `docker attach drogon-dev`.
