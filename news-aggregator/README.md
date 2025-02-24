# 📰 News Aggregator - Dockerized Setup  

This project is a **React-based News Aggregator** that fetches news from multiple sources and displays them in a user-friendly interface. This guide explains how to run the project inside a **Docker container**.  

## 🚀 Getting Started with Docker  

### 📌 Prerequisites  
Ensure you have the following installed on your system:  
- [Docker](https://www.docker.com/get-started)  
- [Docker Compose](https://docs.docker.com/compose/install/)  

### 📂 Project Structure  

news-aggregator/ │── src/ │── public/ │── Dockerfile │── docker-compose.yml │── package.json │── .env │── README.md


## 🔧 **Setup Instructions**  

### 1️⃣ **Clone the Repository**
extract the zip file
cd news-aggregator

2️⃣ Set Up Environment Variables
Create a .env file in the root directory and add your API keys:

REACT_APP_NEWS_API_KEY=ee2e7737dc884462aec5a886fd1161da
REACT_APP_GUARDIAN_API_KEY=29877b91-ca59-4503-aaf0-ccd4c4892b46
REACT_APP_NYT_API_KEY=8b6500b2ab07d0dad20695e890f4f3af

🏗 Running the Application with Docker

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

🛠 Docker Configuration Files
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
Ensure that your .env file is correctly formatted (no quotes around API keys).
If running locally, restart the container after updating .env:

   docker compose down
   docker compose up --build

🔹 Port Already in Use
If port 3000 is in use, stop any running processes or change the port mapping in docker-compose.yml:

ports:
  - "3001:3000"
Then run:
docker compose up --build

----------------------------------------------------------------------------------------------

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
        The Guardian API 🏛️
        New York Times API (NYT) 🏙️
        Implemented Promise.allSettled() to ensure graceful handling of API failures.
        If one API fails, the application still displays results from the other sources.
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

# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).
