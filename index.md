---
layout: default
title: Deploy React + Vite App to GitHub Pages
description: A step-by-step guide to setup and deploy a React + Vite web application to GitHub Pages.
---

# **Introduction**
## **Background Information**
Starting and publishing a frontend project online requires the right tools, and **React + Vite**, hosted for free using **GitHub Pages**, is the perfect combination. 

**Vite** is a modern build tool designed for speed and efficiency, making it an excellent choice for developing React applications. It provides instant server startup, fast hot module replacement (HMR), and optimized production builds.

**React** is a popular JavaScript library used to build interactive user interfaces, enabling developers to create reusable components for dynamic web applications. 

**GitHub Pages** is a free and easy-to-use hosting service that allows developers to deploy static websites directly from a GitHub repository, making it ideal for portfolios, projects, and web experiments.

This guide will walk through the process of deploying a **React + Vite** web application to GitHub Pages.

## **Who is this Guide For?**
This guide is for developers, students, and anyone looking to deploy a frontend app online. Whether you're showcasing a portfolio project, sharing an interactive web app, or simply testing frontend designs, this step-by-step tutorial will help you set up, configure, and publish your project efficiently.

## **Context of Use**
- **For Developers:** Useful for quick prototyping and sharing React applications.
- **For Students:** Helps in publishing academic or portfolio projects without the need for paid hosting.
- **Common Challenges:** Users may face issues related to incorrect configurations, missing dependencies, or incorrect repository setup.

---
# **Requirements**
Before starting, ensure you have the following tools installed and configured on your system.

## **Hardware Requirements:**
- A computer (Windows, macOS, or Linux)
- Stable internet connection

## **Software Requirements:**
1. **Node.js (LTS version)** – Required to run JavaScript applications.
   - Download from: [https://nodejs.org/en/download](https://nodejs.org/en/download)
2. **Git** – Required for version control and pushing code to GitHub.
   - Download from: [https://git-scm.com/downloads](https://git-scm.com/downloads)
3. **GitHub Account** – Needed to create a repository and host the project.
   - Sign up at: [https://github.com](https://github.com)
4. **Code Editor (Recommended: VS Code)** – To code and edit your project.
   - Download from: [https://code.visualstudio.com/Download/](https://code.visualstudio.com/Download)

---
# **Safety Considerations**
- Be cautious when running commands in the terminal to avoid accidental file deletions.
- Ensure that you are working inside the correct directory before executing Git commands.
- Avoid committing sensitive data (e.g., API keys, credentials) to public repositories.
- Regularly update dependencies to prevent security vulnerabilities.

---
# **Step-by-Step Instructions**

## **Step 1: Create a GitHub Repository**
1. Go to GitHub and log in.
2. Click on New Repository.

<figure>
  <img src="./assets/images/github-new-repo.png" alt="GitHub New Repo Button" width="500">
  <figcaption style="font-size: 14px; color: gray;">Figure 1: Creating a new GitHub repository.</figcaption>
</figure>


3. Enter a repository name (e.g., \<your-repo-name\>).
4. Choose Public (or Private if you have GitHub Pro).
5. Do not initialize with a README, .gitignore, or license (these will be added later).
6. Click Create Repository.

<figure>
  <img src="./assets/images/github-create-repo.png" alt="GitHub Create Repo" width="500">
  <figcaption style="font-size: 14px; color: gray;">Figure 2: GitHub interface when creating a repository.</figcaption>
</figure>

## **Step 2: Set Up a React + Vite Project**
1. Open a terminal or command prompt.
2. Navigate to the directory where you want to create the project.

   ```sh
   cd path/to/your/repo
   ```

3. Run the following command to create a new Vite project:

   ```sh
   # Replace <your-project-name> with your desired project name
   npm create vite@latest <your-project-name> -- --template react-ts 
   ```

4. Navigate into the project directory:

   ```sh
   cd <your-project-name>
   ```

5. Install project dependencies:

   ```sh
   npm install
   ```

## **Step 3: Configure Vite for GitHub Pages**
1. Open `vite.config.js` in a code editor.
2. Add the following `base` property to the configuration:

   ```js
   import { defineConfig } from 'vite';
   import react from '@vitejs/plugin-react';

   export default defineConfig({
     plugins: [react()],
     base: '/<your-repo-name>/', // Replace <your-repo-name> with your actual GitHub repository name
   });
   ```

## **Step 4: Modify package.json for Deployment**
1. Open `package.json`.
2. Add this line to the top-level of the file:

   ```json
   "homepage": "https://<your-username>.github.io/<your-repo-name>/",
   ```
2. Add the following scripts inside the `scripts` section:

   ```json
   "predeploy": "npm run build",
   "deploy": "gh-pages -d dist"
   ```
   Below is an example of how your the `package.json` file should look after modification:

   ```json
   {
      "name": "my-vite-app",
      "private": true,
      "version": "0.0.0",
      "type": "module",
      "homepage": "https://anushnandyala.github.io/my-vite-app/", 
      "scripts": {
         "dev": "vite",
         "build": "vite build",
         "lint": "eslint .",
         "preview": "vite preview",
         "predeploy": "npm run build",
         "deploy": "gh-pages -d dist"
      },
      "dependencies": {
         "react": "^19.0.0",
         "react-dom": "^19.0.0"
      },
      "devDependencies": {
         "@eslint/js": "^9.21.0",
         "@types/react": "^19.0.10",
         "@types/react-dom": "^19.0.4",
         "@vitejs/plugin-react": "^4.3.4",
         "eslint": "^9.21.0",
         "eslint-plugin-react-hooks": "^5.1.0",
         "eslint-plugin-react-refresh": "^0.4.19",
         "gh-pages": "^6.3.0",
         "globals": "^15.15.0",
         "vite": "^6.2.0"
      }
   }
   ```

3. Run the following command to install the GitHub Pages package:

   ```sh
   npm install gh-pages --save-dev
   ```

## **Step 5: Initialize Git and Push the Project to GitHub**
1. Initialize a Git repository:

   ```sh
   git init
   ```
2. Add the remote GitHub repository:

   ```sh
   git remote add origin https://github.com/<your-username>/<your-repo-name>.git
   ```
3. Commit and push the code:

   ```sh
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git push -u origin main
   ```
4. Go to `https://github.com/<your-username>/<your-repo-name>` to see your code on GitHub.

<figure>
  <img src="./assets/images/github-vite-repo.png" alt="GitHub Vite Repo" width="500">
  <figcaption style="font-size: 14px; color: gray;">Figure 3: GitHub repository with the Vite project files.</figcaption>
</figure>

## **Step 6: Deploy the App to GitHub Pages**
1. Run the deployment script:

   ```sh
   npm run deploy
   ```
   This builds the project and pushes the `dist/` folder to the `gh-pages` branch.

## **Step 7: Enable GitHub Pages**
1. Navigate to your **GitHub repository** at `https://github.com/<your-username>/<your-repo-name>`.

<figure>
  <img src="./assets/images/github-settings-button.png" alt="GitHub Settings Button" width="500">
  <figcaption style="font-size: 14px; color: gray;">Figure 4: GitHub Settings button for repository configuration.</figcaption>
</figure>

2. Go to **Settings > Pages**.

<figure>
  <img src="./assets/images/github-pages-button.png" alt="GitHub Pages Button" width="300">
  <figcaption style="font-size: 14px; color: gray;">Figure 5: Navigating to the GitHub Pages section in repository settings.</figcaption>
</figure>

3. Under **Branch**, select `gh-pages` and click **Save**.

<figure>
  <img src="./assets/images/github-branch-select.png" alt="GitHub Branch Select" width="500">
  <figcaption style="font-size: 14px; color: gray;">Figure 6: Selecting the `gh-pages` branch for deployment on GitHub Pages.</figcaption>
</figure>

4. Your site will be available at:

   ```
   https://<your-username>.github.io/<your-repo-name>/
   ```

<figure>
  <img src="./assets/images/vite-site.png" alt="Vite Site" width="500">
  <figcaption style="font-size: 14px; color: gray;">Figure 7: Example of a deployed Vite site hosted on GitHub Pages.</figcaption>
</figure>

5. When you make changes to your project, run `npm run deploy` to update the deployed site. Note that this is seperate from pushing changes to the main branch.

## **Step 8 (Optional): Automate Deployment with GitHub Actions**

If you want to deploy to the website everytime you push to the main branch, you can set up a GitHub Action workflow using the following steps. Note that these following steps only work if authenticate to GitHub using a personal access token.

1. Inside your project, create a new folder.

   ```sh
   mkdir -p .github/workflows
   ```
2. Create a new file inside that folder:

   ```sh
   touch .github/workflows/deploy.yml
   ```
3. Open the `deploy.yml` file and add the following content:

   {% raw %}
   ```yml
   name: Deploy to GitHub Pages

   on:
      push:
         branches:
            - main  # Runs when pushing to main

   permissions:
      contents: write  # Ensure GitHub Actions can push to gh-pages

   jobs:
      deploy:
         runs-on: ubuntu-latest

         steps:
            - name: Checkout Repository
              uses: actions/checkout@v4
              with:
                persist-credentials: false  # Important for token-based authentication

            - name: Set up Node.js
              uses: actions/setup-node@v4
              with:
                node-version: 18
                cache: 'npm'

            - name: Install Dependencies
              run: npm install

            - name: Build Project
              run: npm run build

            - name: Deploy to GitHub Pages
              env:
                GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
              run: npm run deploy
   ```
   {% endraw %}
4. Update the `deploy` script in the `package.json` file to:

   ```json
   "deploy": "gh-pages -d dist -u \"github-actions-bot <github-actions@github.com>\" --repo https://x-access-token:${GITHUB_TOKEN}@github.com/<your-username>/<your-repo-name>.git"
   ```

5. Commit and push the changes to main.

   ```sh
   git add .
   git commit -m "Add GitHub Actions auto-deploy workflow"
   git push origin main
   ```

6. Go to the **Actions** tab in your GitHub repository to see the workflow running.

<figure>
  <img src="./assets/images/github-actions.png" alt="GitHub Actions" width="600">
  <figcaption style="font-size: 14px; color: gray;">Figure 8: GitHub Actions workflow running the deployment process.</figcaption>
</figure>

Now, every time you push to the main branch, Github Actions will:
- Install dependencies
- Build your Vite project  
- Deploy the project to GitHub Pages using `gh-pages`

---
# **Conclusion & Further Resources**
You have successfully deployed a **React + Vite** app to **GitHub Pages**! If you encounter issues, here are some additional resources:
- [Vite Documentation](https://vitejs.dev/guide/)
- [GitHub Pages Documentation](https://pages.github.com/)
- [GitHub CLI Documentation](https://cli.github.com/)

For accessibility and further assistance, check **GitHub Discussions** or **Stack Overflow** for troubleshooting common errors.

---
# **References**
Node.js. (n.d.). *Node.js Downloads*. Retrieved March 10, 2025, from [https://nodejs.org/](https://nodejs.org/)

Git. (n.d.). *Git - Downloads*. Retrieved March 10, 2025, from [https://git-scm.com/](https://git-scm.com/)

GitHub Pages. (n.d.). *GitHub Pages - Websites for you and your projects*. Retrieved March 10, 2025, from [https://pages.github.com/](https://pages.github.com/)

Vite. (n.d.). *Vite - Next generation frontend tooling*. Retrieved March 10, 2025, from [https://vitejs.dev/](https://vitejs.dev/)
