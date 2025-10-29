# N8N with Ngrok Setup

This repository contains a Docker Compose setup for running N8N (Nodemation) with Ngrok integration, allowing you to expose your N8N instance to the internet securely.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)
- [Ngrok Account](https://ngrok.com/) (for the authentication token)

## Quick Start

1. Clone this repository:

   ```bash
   git clone <repository-url>
   cd n8n_ngrok_setup
   ```

2. Set up environment variables:

   ```bash
   cp .env.template .env
   ```

   Edit the `.env` file and update the following values:

   - `N8N_EDITOR_BASE_URL`: Your Ngrok URL (will be available after first run)
   - `WEBHOOK_URL`: Same as your Ngrok URL
   - `NGROK_AUTHTOKEN`: Your Ngrok authentication token
   - Adjust other variables as needed (timezone, port, etc.)

3. Start the services:

   ```bash
   docker-compose up -d
   ```

4. Access N8N:
   - The local URL will be: `http://localhost:5555`
   - The Ngrok URL will be displayed in the Ngrok container logs:
     ```bash
     docker-compose logs ngrok
     ```

## Available Scripts

- `start_n8n.bat`: Windows batch file to start the services
  ```bash
  .\start_n8n.bat
  ```

## Configuration

### Environment Variables

- `GENERIC_TIMEZONE`: Set your timezone (default: Asia/Kolkata)
- `TZ`: System timezone (default: Asia/Kolkata)
- `N8N_PORT`: Port for N8N (default: 5555)
- `N8N_EDITOR_BASE_URL`: Your Ngrok URL for the editor
- `WEBHOOK_URL`: Your Ngrok URL for webhooks
- `NGROK_AUTHTOKEN`: Your Ngrok authentication token

For all available environment variables, check the `.env.template` file.

## Architecture

The setup consists of two main services:

1. **N8N Service**:

   - Runs the main N8N application
   - Persists data using Docker volumes
   - Configurable through environment variables

2. **Ngrok Service**:
   - Provides secure tunneling to your N8N instance
   - Enables webhook functionality
   - Auto-connects to N8N service

## Data Persistence

N8N data is persisted using Docker volumes:

- `n8n_data`: Stores all N8N workflows, credentials, and settings

## Network

Services are connected through a Docker bridge network (`n8n_net`), ensuring secure communication between N8N and Ngrok.

## Troubleshooting

1. **Ngrok Connection Issues**:

   - Verify your Ngrok auth token in the `.env` file
   - Check Ngrok logs: `docker-compose logs ngrok`

2. **N8N Access Issues**:

   - Ensure ports are not in use: `netstat -ano | findstr 5555`
   - Check N8N logs: `docker-compose logs n8n`

3. **Container Start Issues**:
   - Ensure Docker is running
   - Try stopping and removing containers:
     ```bash
     docker-compose down
     docker-compose up -d
     ```

## Security Considerations

- The `.env` file contains sensitive information - never commit it to version control
- Always use strong passwords and secure tokens
- Regularly update your Docker images for security patches

## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a new Pull Request

## License

This project is open-source and available under the MIT License.

## Support

If you encounter any issues or need support, please open an issue in the GitHub repository.
