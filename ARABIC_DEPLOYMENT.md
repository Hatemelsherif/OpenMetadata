# OpenMetadata with Arabic Language Support

This repository contains OpenMetadata with comprehensive Arabic language support, built and deployed using GitHub Actions.

## Features

- ✅ Complete Arabic UI translation (2,571 keys)
- ✅ RTL (Right-to-Left) layout support via Ant Design
- ✅ Automated Docker builds via GitHub Actions
- ✅ Published to GitHub Container Registry
- ✅ Based on OpenMetadata 1.9.11 stable release

## Quick Start

### Prerequisites

- Docker and Docker Compose installed
- Internet connection to pull images

### Deployment

1. **Pull the latest image:**
   ```bash
   docker pull ghcr.io/hatemelsherif/openmetadata-arabic:1.9.11-arabic
   ```

2. **Start OpenMetadata:**
   ```bash
   docker-compose -f docker-compose-arabic.yml up -d
   ```

3. **Access the application:**
   - URL: http://localhost:8585
   - Default credentials:
     - Username: `admin`
     - Password: `admin`

4. **Switch to Arabic:**
   - Click on user profile (top right)
   - Select Settings
   - Choose Language → العربية (ar-SA)

### Stopping the Application

```bash
docker-compose -f docker-compose-arabic.yml down
```

### Removing All Data

```bash
docker-compose -f docker-compose-arabic.yml down -v
```

## Architecture

### Components

- **MySQL 8.0**: Metadata storage database
- **Elasticsearch 7.17**: Search and indexing engine
- **OpenMetadata Server**: Main application with Arabic UI

### Docker Image

The Docker image is automatically built by GitHub Actions on every push to `stable-1.9.11` branch:

- **Registry**: GitHub Container Registry (ghcr.io)
- **Image**: `ghcr.io/hatemelsherif/openmetadata-arabic:1.9.11-arabic`
- **Build**: https://github.com/Hatemelsherif/OpenMetadata/actions

## Development

### Building Locally

If you want to build the image locally:

```bash
docker build -f Dockerfile.arabic -t openmetadata-arabic:local .
```

### Customizing Translations

1. Edit the translation file:
   ```bash
   openmetadata-ui/src/main/resources/ui/src/locale/languages/ar-sa.json
   ```

2. Commit and push to trigger automated build:
   ```bash
   git add openmetadata-ui/src/main/resources/ui/src/locale/languages/ar-sa.json
   git commit -m "Update Arabic translations"
   git push origin stable-1.9.11
   ```

3. Wait for GitHub Actions to build (~20 minutes)

4. Pull the new image:
   ```bash
   docker pull ghcr.io/hatemelsherif/openmetadata-arabic:1.9.11-arabic
   docker-compose -f docker-compose-arabic.yml up -d
   ```

## Updating from Upstream

To get the latest OpenMetadata updates:

```bash
# Add upstream if not already added
git remote add upstream https://github.com/open-metadata/OpenMetadata.git

# Fetch latest changes
git fetch upstream

# Merge upstream stable release into your branch
git checkout stable-1.9.11
git merge upstream/stable-1.9.11

# Resolve any conflicts, then push
git push origin stable-1.9.11
```

GitHub Actions will automatically rebuild the image with your Arabic customizations on top of the latest upstream changes.

## Troubleshooting

### Image Pull Errors

If you get permission errors pulling from ghcr.io:

```bash
# Make sure the repository is public, or authenticate:
echo $GITHUB_PAT | docker login ghcr.io -u USERNAME --password-stdin
```

### Database Migration Issues

If the application fails to start due to database issues:

```bash
# Remove volumes and restart
docker-compose -f docker-compose-arabic.yml down -v
docker-compose -f docker-compose-arabic.yml up -d
```

### Port Conflicts

If port 8585 is already in use, edit `docker-compose-arabic.yml`:

```yaml
ports:
  - "8586:8585"  # Change left side to available port
```

## License

Same as OpenMetadata - Apache License 2.0

## Credits

- Based on [OpenMetadata](https://github.com/open-metadata/OpenMetadata)
- Arabic translation and RTL support by Hatem Elsherif
- Built with [Claude Code](https://claude.com/claude-code)
