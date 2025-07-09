# Project Brief: ngLibrary (Angular Reference Application)

## Overview
The **ngLibrary** project is a reference Angular application that demonstrates modern web application architecture and development practices. It implements a full-featured e-commerce website for a bookstore and serves as a practical example for developers building scalable and maintainable applications with Angular.

## Purpose
The primary goals of the ngLibrary project are to:
- Showcase best practices in Angular application development.
- Demonstrate the use of **NgRx** for state management in a real-world application.
- Provide a hands-on learning tool for developers exploring reactive programming, component-based architecture, and comprehensive testing strategies.

## Key Features
- **Architecture**: Feature-based, reactive architecture using NgRx for state management. It follows a clear separation of concerns with smart (container) and UI (presentational) components.
- **Frontend**: Built with **Angular 11** and TypeScript.
- **Backend Integration**: Fetches book data from the public **Open Library API**.
- **Comprehensive Testing**: Includes unit tests with **Jest** and end-to-end tests with **Cypress**.
- **Component-Driven Development**: Uses **Storybook** to develop and showcase UI components in isolation.
- **Performance Optimizations**:
  - Implements **lazy loading** for feature modules to improve initial load time.
  - Uses `PreloadAllModules` strategy to preload lazy-loaded modules in the background.

## Technology Stack
- Angular 11
- NgRx (for state management)
- RxJS
- TypeScript
- Jest (for unit testing)
- Cypress (for end-to-end testing)
- Storybook (for UI component development)

## Getting Started
To run the ngLibrary project:
1. Clone the repository: `git clone https://github.com/mrWh1te/ngLibrary.git`
2. Install prerequisites:
   - Node.js
   - Angular CLI
3. Install dependencies: `npm install`
4. Run the development server: `npm start`
5. To run tests: `npm test`
6. To view components in Storybook: `npm run storybook` 