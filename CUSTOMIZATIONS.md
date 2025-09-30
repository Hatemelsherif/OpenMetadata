# OpenMetadata Customizations

This document tracks all customizations made to the OpenMetadata platform for **hatemelsherif** organization.

## Repository Setup

- **Upstream Repository**: https://github.com/open-metadata/OpenMetadata
- **Fork Repository**: https://github.com/Hatemelsherif/OpenMetadata
- **Base Version**: 1.10.0-SNAPSHOT
- **Custom Branch**: `custom-main`

## Git Workflow

### Keeping Sync with Upstream

```bash
# Fetch upstream changes
git fetch upstream

# Update main branch (mirror of upstream)
git checkout main
git merge upstream/main --ff-only
git push origin main

# Merge into custom branch
git checkout custom-main
git merge main
# Resolve conflicts if any
git push origin custom-main
```

### Feature Development

```bash
# Create feature branch from custom-main
git checkout custom-main
git checkout -b feature/your-feature-name

# Work on your feature
# ... make changes ...

# Commit and push
git add .
git commit -m "feat: description of your feature"
git push origin feature/your-feature-name

# Create PR to custom-main branch
```

## Customization Areas

### 1. Branding & UI Customizations

**Status**: Not Started

**Location**: `openmetadata-ui/src/main/resources/ui/src/`

**Planned Changes**:
- [ ] Update application logo and favicon
- [ ] Customize color scheme and theme
- [ ] Update company branding in headers/footers
- [ ] Customize welcome messages

**Files to Modify**:
- `constants/constants.ts` - Application constants
- `assets/` - Logo and image files
- `styles/` - Theme and styling files

---

### 2. Custom Connectors

**Status**: Not Started

**Location**: `ingestion/src/metadata/ingestion/source/`

**Planned Changes**:
- [ ] Add connector for internal data systems
- [ ] Extend existing connectors with custom metadata

**Implementation Notes**:
- Follow existing connector patterns
- Add tests in `ingestion/tests/`
- Update `setup.py` with new dependencies

---

### 3. Custom Authentication

**Status**: Not Started

**Location**: `openmetadata-service/src/main/java/org/openmetadata/service/security/`

**Planned Changes**:
- [ ] Integrate with internal SSO system
- [ ] Add custom authentication handlers
- [ ] Configure JWT token settings

**Configuration**:
- Update `conf/openmetadata.yaml`
- Use environment variables for secrets

---

### 4. Custom Policies & Governance Rules

**Status**: Not Started

**Location**: `openmetadata-service/src/main/java/org/openmetadata/service/governance/`

**Planned Changes**:
- [ ] Add organization-specific governance rules
- [ ] Custom data classification policies
- [ ] Domain-specific validation rules

---

### 5. Custom Applications

**Status**: Not Started

**Location**: `openmetadata-ui/src/main/resources/ui/src/pages/Applications/`

**Planned Changes**:
- [ ] Build custom data quality dashboards
- [ ] Add organization-specific data apps
- [ ] Integrate with internal tools

---

## Version History

### v1.10.0-custom-1 (Planned)
- Initial fork setup
- Documentation created
- Development environment configured

---

## Build & Deployment

### Local Development

```bash
# Prerequisites check
make prerequisites

# Install dependencies
make install_dev_env
make yarn_install_cache

# Run locally with Docker
./docker/run_local_docker.sh -m ui -d mysql

# Frontend development
cd openmetadata-ui/src/main/resources/ui
yarn start
```

### Production Build

```bash
# Full build
mvn clean install -DskipTests

# Create custom Docker image
docker build -t hatemelsherif/openmetadata:1.10.0-custom-1 .
docker push hatemelsherif/openmetadata:1.10.0-custom-1
```

### Testing

```bash
# Run all tests
mvn test
cd openmetadata-ui/src/main/resources/ui && yarn test
cd ingestion && pytest

# E2E tests
make run_e2e_tests
```

---

## Merge Conflict Resolution Strategy

### High-Priority Files (Review Carefully)
- `pom.xml` - Dependency versions
- `package.json` - Frontend dependencies
- `setup.py` - Python dependencies
- `openmetadata-spec/` - Schema definitions
- Database migration files

### Resolution Steps
1. Always test after merging upstream changes
2. Run full test suite before pushing
3. Document any breaking changes
4. Update this file with merge notes

---

## CI/CD Pipeline

**Status**: Not Configured

**Planned**:
- [ ] GitHub Actions for automated testing
- [ ] Docker image building
- [ ] Automated deployment to staging
- [ ] Production deployment process

---

## Notes & Warnings

### ⚠️ Do NOT Modify Directly
- `ingestion/src/metadata/generated/` - Auto-generated from schemas
- `openmetadata-ui/src/main/resources/ui/src/generated/` - Auto-generated
- Database migration files in `bootstrap/sql/migrations/` (create new ones instead)

### ✅ Safe to Modify
- Configuration files (`conf/`)
- Custom connectors (new files only)
- UI components and styling
- Documentation files

### 🔄 Requires Schema Regeneration
If you modify files in `openmetadata-spec/`, run:
```bash
mvn clean install -DskipTests
make generate
```

---

## Contact & Support

**Maintainer**: hatemelsherif
**Fork Repository**: https://github.com/Hatemelsherif/OpenMetadata
**Issue Tracking**: GitHub Issues in fork repository

---

## Upstream Sync Log

### 2025-09-30
- Initial fork created from upstream main branch
- Version: 1.10.0-SNAPSHOT (commit: d0074d748a)
- Configured git remotes
- Created custom-main branch

---

## TODO

- [ ] Set up local development environment
- [ ] Verify all prerequisites installed
- [ ] Run application locally
- [ ] Plan first customization
- [ ] Set up CI/CD pipeline
- [ ] Create staging environment
- [ ] Document deployment procedures