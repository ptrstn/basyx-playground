
# BaSyx Playground

This repository provides a quick way to set up and experiment with the [Eclipse BaSyx](https://www.eclipse.org/basyx/) framework for Industry 4.0 Asset Administration Shell (AAS) implementations.

## Overview

The BaSyx Playground includes a Docker Compose configuration that sets up a complete BaSyx environment with the following components:

- **AAS Environment**: A server for storing and managing Asset Administration Shells and Submodels
- **AAS Registry**: A registry service for registering and discovering AAS instances
- **Submodel Registry**: A registry service for Submodels
- **AAS GUI**: A web interface for exploring and interacting with the AAS environment

## Getting Started

### Prerequisites

- [Git](https://git-scm.com/)
- [Docker](https://www.docker.com/)

> ℹ️ You can also use alternative container platforms like [Rancher Desktop](https://rancherdesktop.io/) or [Podman](https://podman.io/).

### Setup

Clone the repository:

```bash
git clone https://github.com/ptrstn/basyx-playground.git
cd basyx-playground
```

Start the BaSyx environment:

```bash
docker compose up -d
```

That's it! The BaSyx environment is now running.

## Adding AAS Files

Place your AAS files (`.xml`, `.json`, or `.aasx`) in the `aas` folder. 
These files will be automatically uploaded to the BaSyx server when starting the environment with `docker compose up -d`.

This configuration mounts the local `aas` directory to `/application/aas` inside the container, and the `BASYX_ENVIRONMENT` setting tells BaSyx to load AAS files from this location.

```yaml
services:
  aas-environment:
    # ...
    environment:
      BASYX_ENVIRONMENT: file:/application/aas
    volumes:
      - ./aas:/application/aas
```

The repository already includes sample AAS files:
- `WST_A_1.aasx`
- `Semitrailer.json`

## Accessing the Services

Once the environment is running, you can access the following services:

- **AAS GUI**: http://localhost:3000/swagger-ui/index.html
- **AAS Environment**: http://localhost:8081/swagger-ui/index.html
- **AAS Registry**: http://localhost:8082/swagger-ui/index.html
- **Submodel Registry**: http://localhost:8083/swagger-ui/index.html

## API Endpoints

The environment exposes the following API endpoints:

- AAS Repository: [http://localhost:8081/shells](http://localhost:8081/shells)
- Submodel Repository: [http://localhost:8081/submodels](http://localhost:8081/submodels)
- AAS Registry: [http://localhost:8082/shell-descriptors](http://localhost:8082/shell-descriptors)
- Submodel Registry: [http://localhost:8083/submodel-descriptors](http://localhost:8083/submodel-descriptors)

## Stopping the Environment

To stop the environment:

```bash
docker compose down
```