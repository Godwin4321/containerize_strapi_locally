# Strapi Internship Task

## Overview
This project demonstrates a local setup of a **Strapi Headless CMS** application created as part of an internship task. The system provides a backend service with an admin panel, a local database, and automatically generated APIs for managing content.

---

## Tech Stack
- Node.js 20
- Strapi v5
- SQLite
- Git & GitHub
- Linux

---

## Prerequisites
Make sure you have the following installed:

- **Node.js v20 or higher**
  ```bash
  node --version
npm

npm --version
Git

git --version

Setup Instructions
1. Clone the Repository
git clone <repo_url>

2. Install Dependencies
npm install

3. Start the Application
npm run develop


Once running, open the admin panel at:

http://localhost:1337/admin

Admin Setup

On first launch:

Create an admin user

Log in to the Strapi dashboard

Custom Content Type
Blog

Fields:

title (Text)

description (Rich Text)

publishedDate (Date)

A sample blog entry was created to verify database connectivity and API functionality.

Project Approach

This project was scaffolded using the official Strapi project generator, which created a complete backend service including configuration, database setup, admin panel, and API support.

The system was then configured via the admin panel by defining a custom Blog content type and creating sample data to demonstrate content management functionality.