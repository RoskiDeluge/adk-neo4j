# ADK Neo4j Integration

This repository contains Jupyter notebooks for working with Google ADK (Agent Development Kit) and Neo4j graph database integration.

## Setup

This project uses [uv](https://docs.astral.sh/uv/) for dependency management and virtual environment handling.

### Prerequisites

- Python 3.11 or higher
- [uv package manager](https://docs.astral.sh/uv/getting-started/installation/)

### Installation

1. Clone the repository and navigate to the project directory:
   ```bash
   cd adk-neo4j
   ```

2. Install dependencies using uv:
   ```bash
   uv sync
   ```

3. The project is now ready to use!

## Neo4j Database Setup

This project requires a Neo4j database with the APOC plugin. The easiest way to set this up is using Docker.

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/) installed on your system

### Setting up Neo4j with Docker

1. **Create and start the Neo4j container:**
   ```bash
   docker run -d \
     --name neo4j-adk \
     -p 7474:7474 -p 7687:7687 \
     -v neo4j_data:/data \
     -v neo4j_logs:/logs \
     -v neo4j_import:/var/lib/neo4j/import \
     -v neo4j_plugins:/plugins \
     -e NEO4J_AUTH=neo4j/password123 \
     -e NEO4J_PLUGINS='["apoc"]' \
     -e NEO4J_dbms_security_procedures_unrestricted='apoc.*' \
     -e NEO4J_dbms_security_procedures_allowlist='apoc.*' \
     neo4j:5.15
   ```

2. **Create environment file:**
   Create a `.env` file in the project root with the following content:
   ```
   NEO4J_URI=bolt://localhost:7687
   NEO4J_USERNAME=neo4j
   NEO4J_PASSWORD=password123
   NEO4J_DATABASE=neo4j
   ```

3. **Verify the setup:**
   - Neo4j web interface: http://localhost:7474
   - Username: `neo4j`
   - Password: `password123`

### Managing the Neo4j Container

```bash
# Check if container is running
docker ps

# View Neo4j logs
docker logs neo4j-adk

# Stop the database
docker stop neo4j-adk

# Start the database
docker start neo4j-adk

# Remove the container (if needed)
docker rm neo4j-adk
```

## Running Jupyter Notebooks

To run the Jupyter notebooks in this project:

```bash
# Start Jupyter Lab
uv run jupyter lab

# Or start Jupyter Notebook
uv run jupyter notebook
```

The notebooks will automatically use the correct Python environment with all the required dependencies:

- `google-adk==1.5.0` - Google Agent Development Kit
- `neo4j==5.28.1` - Neo4j Python driver
- `litellm==1.73.6` - LiteLLM for various AI models
- `jupyter>=1.0.0` - Jupyter notebook environment
- `ipykernel>=6.0.0` - IPython kernel for Jupyter
- `notebook>=7.0.0` - Jupyter notebook interface

## Available Notebooks

- `intro_to_adk_1.ipynb` - Introduction to ADK with Neo4j integration

## Project Structure

```
adk-neo4j/
├── .venv/                  # Virtual environment (created by uv)
├── helper.py              # Helper functions
├── neo4j_for_adk.py       # Neo4j integration utilities
├── intro_to_adk_1.ipynb   # Main tutorial notebook
├── pyproject.toml         # Project configuration and dependencies
├── uv.lock               # Locked dependency versions
└── README.md             # This file
```

## Development

To add new dependencies:

```bash
uv add package-name
```

To run Python scripts directly:

```bash
uv run python script_name.py
```

To activate the virtual environment in your shell:

```bash
source .venv/bin/activate  # On macOS/Linux
```
