# JavaScript/Typescript Testing Guides

A modern, responsive web application that provides comprehensive documentation and examples for JavaScript/Typescript testing concepts.

## Live Demo

The application is hosted and can be accessed at: [http://23.111.144.154:3005/](http://23.111.144.154:3005/)

## Features

- 📚 Comprehensive testing guides covering:
  - Global Functions
  - Assertions & Matchers
  - Mocking Functions
  - Timer & Date Mocks
  - Module Mocking
  - Spying
  - Snapshot Testing
  - Asynchronous Testing


## Prerequisites

- Node.js (v14 or higher)
- Docker and Docker Compose (for containerized deployment)

## Installation

### Local Development

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd testing-guides
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the development server:
   ```bash
   npm start
   ```

4. Open your browser and visit:
   ```
   http://localhost:3000
   ```

### Docker Deployment

1. Build and start the containers:
   ```bash
   docker-compose up --build
   ```

2. Access the application at:
   ```
   http://localhost:3005
   ```

## Project Structure

```
testing-guides/
├── testing_guides/          # Markdown content files
│   ├── 1_global_functions.md
│   ├── 2_assertions_and_matchers.md
│   └── ...
├── index.html              # Main application file
├── server.js              # Simple Node.js server
├── package.json           # Project dependencies
├── Dockerfile            # Docker configuration
├── docker-compose.yml    # Docker Compose configuration
└── README.md            # Project documentation
```