# UD2 Project

A multi-module IntelliJ IDEA project that manages several interconnected applications including a Java web server, frontend dashboards, and database management tools.

## Quick Start

### Prerequisites

- **IntelliJ IDEA** (Community or Ultimate Edition)
- **Java Development Kit** (JDK 24 or compatible)
- **Node.js** (for frontend development)
- **Maven** (for Java project management)
- **Git** (for version control)

### Getting Started

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd UD2
   ```

2. **Open in IntelliJ IDEA**:
   - Launch IntelliJ IDEA
   - Select "Open" from the welcome screen
   - Navigate to the `UD2` directory
   - Select the `UD2.iml` file or the entire `UD2` folder
   - Click "OK"

3. **Configure Project Settings**:
   - IntelliJ will automatically detect the project structure
   - Ensure the correct JDK is selected (JDK 24 recommended)
   - Maven dependencies will be automatically resolved

4. **Set up the development environment**:
   - Ensure all parent directories (`../Kof22/`, `../QRun-IO/`) exist
   - Run the `ServerAndFrontend` configuration to start development

## Repository Structure

This git repository serves as a coordination point for multiple related applications:

```
UD2/
├── README.md              # This file
├── UD2.iml               # IntelliJ IDEA project file
└── log/                  # Log files
    └── qqq.log
```

### Related Projects

The UD2 project coordinates with several external applications:

- **Kof22 Website**: Java-based web server (`../Kof22/Website/`)
- **QQQ Frontend Dashboard**: React-based frontend (`../QRun-IO/qqq-frontend-material-dashboard/`)
- **QQQ Backend**: Java middleware (`../QRun-IO/qqq/`)

> **Note**: These external projects should be located in the parent directories as shown above for the IntelliJ run configurations to work properly.

## Run Configurations

The project includes several pre-configured run targets accessible through the IntelliJ run configuration dropdown:

### Java Application Configurations

#### `ServerOnly`
- **Purpose**: Runs only the Java web server
- **Environment**: Development mode (`QQQ_DEPLOYMENT=dev`)
- **Main Class**: `com.kof22.website.Server`
- **Working Directory**: `../Kof22/Website`
- **Access URL**: `http://localhost:8000/admin/`

#### `ServerAndFrontend`
- **Purpose**: Runs both server and frontend with automatic browser launch
- **Environment**: Development mode
- **Prerequisites**: 
  - Kills existing Chrome processes
  - Builds frontend assets before server start
- **Access URL**: `http://localhost:8000/admin/`
- **JDK**: OpenJDK 24

### Frontend Development Configurations

#### `FrontDev`
- **Purpose**: Frontend development server with hot reload
- **Type**: NPM script runner
- **Script**: `dev`
- **Access URL**: `http://localhost:5173`
- **Features**: Auto-opens browser with debugger

#### `Start QQQ Dashboard`
- **Purpose**: Starts the QQQ Material Dashboard
- **Type**: NPM script runner
- **Script**: `start`
- **Access URL**: `http://localhost:3000/`

### Build and Deployment Configurations

#### `clean-and-install`
- **Purpose**: Cleans and installs frontend dependencies
- **Type**: NPM script runner
- **Script**: `clean-and-install`

#### `build-and-publish`
- **Purpose**: Builds and publishes frontend assets
- **Type**: NPM script runner
- **Script**: `build-and-publish`

#### `qqq-install-locally`
- **Purpose**: Maven clean, package, and install for QQQ backend
- **Type**: Maven configuration
- **Goals**: `clean package install -Dmaven.test.skip=true`
- **Working Directory**: `../QRun-IO/qqq`

### Database Management Configurations

#### `dbupdate`
- **Purpose**: Updates database schema using Liquibase
- **Type**: Maven configuration
- **Goals**: `liquibase:update -Dliquibase.contexts=dev`
- **Working Directory**: `../Kof22/Website`

#### `dbdropAndUpdate`
- **Purpose**: Drops and recreates database schema
- **Type**: Maven configuration

#### `dbdropall`
- **Purpose**: Drops all database tables
- **Type**: Maven configuration

### Utility Configurations

#### `Kill Chrome`
- **Purpose**: Terminates all Chrome browser processes
- **Type**: Shell script

#### `Generate QQQ API (openapi.json)`
- **Purpose**: Generates OpenAPI specification
- **Type**: Shell script

## Usage Instructions

### Development Workflow

1. **Start Development Environment**:
   - Run `ServerAndFrontend` for full-stack development
   - Or run `ServerOnly` + `FrontDev` separately for more control

2. **Frontend Development**:
   - Use `FrontDev` for hot-reload development
   - Use `Start QQQ Dashboard` for the Material Dashboard

3. **Database Management**:
   - Run `dbupdate` to apply schema changes
   - Use `dbdropAndUpdate` for fresh database setup

4. **Build and Deploy**:
   - Run `qqq-install-locally` to build backend
   - Use `build-and-publish` for frontend deployment

### Running Configurations

1. **Via IntelliJ UI**:
   - Click the run configuration dropdown in the toolbar
   - Select desired configuration
   - Click the green "Run" button or press `Ctrl+F10` (Windows/Linux) / `Cmd+R` (Mac)

2. **Via Run Menu**:
   - Go to `Run` → `Edit Configurations...`
   - Select and modify configurations as needed
   - Use `Run` → `Run '[Configuration Name]'`

## Environment Variables

- `QQQ_DEPLOYMENT`: Set to `dev` for development mode
- `QFMD_APP_BASE_PATH`: Set to `/admin` for application base path

## Git Workflow

### Branch Management

- **`develop`**: Main development branch
- **`main`**: Production-ready releases
- **Feature branches**: Create from `develop` for new features

### Common Git Commands

```bash
# Check status
git status

# Switch to develop branch
git checkout develop

# Pull latest changes
git pull origin develop

# Create a new feature branch
git checkout -b feature/your-feature-name

# Commit changes
git add .
git commit -m "Your commit message"

# Push changes
git push origin your-branch-name
```

## Troubleshooting

### Project Setup Issues
- **Module not found**: Ensure all parent directories (`../Kof22/`, `../QRun-IO/`) exist
- **JDK issues**: Verify JDK 24 is installed and selected in project settings
- **Maven issues**: Check Maven settings and ensure all dependencies are resolved
- **Node.js issues**: Verify Node.js is installed and accessible from IntelliJ

### Git Issues
- **Repository not found**: Ensure you've cloned the repository correctly
- **Permission denied**: Check your git credentials and repository access
- **Merge conflicts**: Resolve conflicts in IntelliJ or use `git status` to identify conflicted files

## Contributing

1. **Fork the repository** (if you don't have write access)
2. **Create a feature branch** from `develop`
3. **Make your changes** and test thoroughly
4. **Commit your changes** with descriptive messages
5. **Push to your branch** and create a pull request
6. **Request review** from team members

### Commit Message Guidelines

- Use clear, descriptive commit messages
- Start with a verb in imperative mood (e.g., "Add", "Fix", "Update")
- Include context when necessary
- Keep the first line under 50 characters

## Additional Notes

- The project uses Maven for Java dependency management
- Frontend projects use npm for package management
- Database migrations are handled by Liquibase
- The project supports both development and production configurations
- This repository serves as a coordination point for multiple related projects