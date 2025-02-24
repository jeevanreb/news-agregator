📰 News Aggregator - Dockerized Setup

This project is a React-based News Aggregator that fetches news from multiple sources and displays them in a user-friendly interface. This guide explains how to run the project inside a Docker container.

🚀 Getting Started with Docker

📌 Prerequisites

Ensure you have the following installed on your system:

Docker

Docker Compose

📂 Project Structure

news-aggregator/
│── src/
│── public/
│── Dockerfile
│── docker-compose.yml
│── package.json
│── .env
│── README.md

🔧 Setup Instructions

1️⃣ Clone the Repository
clone the project from here

cd news-aggregator

2️⃣ Set Up Environment Variables

Create a .env file in the root directory and add your API keys:

REACT_APP_NEWS_API_KEY=ee2e7737dc884462aec5a886fd1161da
REACT_APP_GUARDIAN_API_KEY=29877b91-ca59-4503-aaf0-ccd4c4892b46
REACT_APP_NYT_API_KEY=8b6500b2ab07d0dad20695e890f4f3af

🏰 Running the Application with Docker

▶️ Using Docker (Without Compose)

Build the Docker Image

docker build -t news-aggregator .

Run the Container

docker run -p 3000:3000 --env-file .env news-aggregator

Access the Application

Open your browser and go to:

http://localhost:3000

▶️ Using Docker Compose (Recommended)

Start the Application

docker compose up

Stop the Application

docker compose down

🦜 Docker Configuration Files

📄 Dockerfile

# Use Node.js image
FROM node:22-alpine

# Set working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package*.json .
RUN npm install

# Copy all files
COPY . .

# Expose port
EXPOSE 3000

# Start the React app
CMD ["npm", "start"]

📄 docker-compose.yml

version: '3.8'
services:
  frontend:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "3000:3000"
    volumes:
      - .:/app
      - /app/node_modules
    env_file:
      - .env

❓ Troubleshooting

🔹 API Key Issues

Ensure that your .env file is correctly formatted (no quotes around API keys). If running locally, restart the container after updating .env:

docker compose down
docker compose up --build

🔹 Port Already in Use

If port 3000 is in use, stop any running processes or change the port mapping in docker-compose.yml:

ports:
  - "3001:3000"

Then run:

docker compose up --build

✅ Key Features Implemented

📌 1. Article Search & Filtering

Users can search for articles by keyword.

Articles can be filtered by category, date, and source.

The search query is sent as a parameter to the service instead of routing to a new page.

📌 2. Personalized News Feed

Users can select preferred sources, categories, and authors from the Settings page.

Preferences are stored in localStorage, ensuring a customized experience when users return.

📌 3. Multiple Data Sources (At Least Three)

Integrated news data from the following sources:

NewsAPI.org 📰

The Guardian API 🏠

New York Times API (NYT) 🌆

Implemented Promise.allSettled() to ensure graceful handling of API failures. If one API fails, the application still displays results from the other sources.

📌 4. Mobile-Responsive Design

Built with Tailwind CSS, ensuring a responsive and modern UI.

The UI adapts seamlessly to mobile, tablet, and desktop screens.

📌 5. API Handling & Error Management

Graceful API failure handling: If an API fails, the app still loads available data.

Displays "No data found" if no articles are available.

Shows a shimmer loading effect while fetching articles instead of a simple "Loading..." text.

📌 6. Performance Optimization & Best Practices

Follows best practices like:

DRY (Don't Repeat Yourself) ✅

KISS (Keep It Simple, Stupid) ✅

SOLID Principles ✅

📌 7. Docker Containerization & Documentation

Dockerized the application to ensure consistent deployment.

Created a Dockerfile and docker-compose.yml for easy setup.

Detailed README.md included, explaining how to:

Build & run the application in Docker.

Set up environment variables.

Troubleshoot common issues.

📌 8. Navigation & Routing

Implemented React Router for navigation.

Users can browse different categories via a dynamic route (/category/:category).

Clicking an article opens it in a new tab while keeping the news aggregator running.

🏆 Additional Enhancements

Shimmer loading effect implemented with Tailwind CSS.

Error boundary handling for API failures.

Optimized API calls to prevent excessive requests.

🌐 Getting Started with Create React App

This project was bootstrapped with Create React App.

Available Scripts

npm start

Runs the app in development mode.
Open http://localhost:3000 to view it in the browser.

npm test

Launches the test runner in interactive watch mode.

npm run build

Builds the app for production to the build folder.

npm run eject

Removes Create React App's default configurations and dependencies, giving full control over the setup.

Learn More

Check out the React documentation for more details.

