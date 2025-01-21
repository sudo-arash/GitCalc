# GitCalc

GitCalc is a simple web application that fetches GitHub repository information through the Github's API. This project allows you to search for repositories on GitHub by specifying the owner and the repository name.

## Features

- Fetch GitHub repository details including:
  - Repository owner
  - Repository name
  - Default branch
  - Fork status
  - Watchers count
  - Stars count
  - Size (in KB)
  - Creation and update date
  - Repository description
- Simple interface
- Loading spinner during data fetch
- Modal to display detailed repository information

## Prerequisites

Before running this project, make sure you have the following installed:

- Node.js (with **bun**)
- TypeScript

## Installation

1. Clone this repository to your local machine:

   ```bash
   git clone https://github.com/sudo-arash/GitCalc.git
   ```

2. Navigate to the project directory:

   ```bash
   cd GitCalc
   ```

3. Install the dependencies:

   ```bash
   bun install
   ```

## Usage

1. Run the development server:

   ```bash
   bun dev
   ```

2. Open your browser and navigate to [http://localhost:5173](http://localhost:5173) to use the GitCalc app.

3. Enter the repository owner and name in the provided form and click on **Fetch Info** to retrieve the repository details.

4. The repository information will be displayed in a modal upon successful fetch.

## Technologies Used

- **Svelte**: For building the user interface.
- **Tailwind CSS**: For styling the app with utility-first classes.
- **Axios**: For making HTTP requests to the GitHub API.
- **Font Awesome**: For icons used throughout the app.
- and the lovely **Bun**.


## The reason behind this project

If you have already guessed by the name, this project was meant to calculate the size of a GitHub REPO. Because I used Github's API all the time to get the size of repos where I had planned to clone, so I decided
to make something like this. This project helps me and probably you.

I hope you like it. If you do, please star and fork the repo to help me out with it.

Cheers everybody!
