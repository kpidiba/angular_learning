# Angular Application Deployment Guide

## Building the Application for Deployment

Deploying an Angular application starts with building it for production. The Angular CLI compiles your TypeScript code, performs optimizations (tree-shaking, minification, AOT compilation, etc.), and outputs the result to a `dist/` folder.

### Production Build Command

Use the following command to create an optimized production build:

```bash
ng build --configuration production
```

Or using the shorthand (still supported):

```bash
ng build --prod
```

> **Note**: In modern Angular versions (v17+), running ng build without a configuration often defaults to production optimizations. However, explicitly using --configuration production is recommended for clarity and to ensure all production-specific settings (like file replacements from environment.prod.ts) are applied.

This command:

- Enables production mode
- Minifies and optimizes bundles
- Removes development-only code
- Generates static files ready for hosting

### Building for Different Environments

Define multiple environments in angular.json under the configurations section (e.g., development, qa, staging, production).

Example command for a custom environment:

```bash
ng build --configuration=qa
```

**Example environments**:

- dev / development — for local testing
- qa — for quality assurance/testing
- prod / production — for live deployment

Each configuration can replace environment files, set different API endpoints, enable/disable features, etc.

### Configuring Base HREF

If your app is deployed in a subdirectory (e.g., https://example.com/my-app/), set the baseHref:

In angular.json:

```bash
"architect": {
  "build": {
    "options": {
      "baseHref": "/my-app/"
    },
    "configurations": {
      "production": {
        "baseHref": "/my-app/"
      }
    }
  }
}
```

You can also override it at build time:

```bash
ng build --base-href /my-app/
```

## Serving the Built Application Locally

To test your production build locally:

1. Install a lightweight static server (recommended):
   
   ```bash
   npm install -g http-server
   ```

2. Navigate to your project root and run:
   
   ```bash
   http-server dist/your-project-name -p 8080
   ```

Replace your-project-name with the actual folder name inside dist/.

Open http://localhost:8080 in your browser to preview the app.

> **Tip**: For more advanced local testing, you can use serve (npm install -g serve) or live-server.

## Server Configuration for Production

Angular is a Single Page Application (SPA), so all routes must fallback to index.html to support client-side routing (Angular Router).

### Common Server Configurations

- **Nginx** (recommended for performance):
  
  ```nginx
  location / {
    try_files $uri $uri/ /index.html;
  }
  ```

- Enable Gzip/Brotli compression and set long-term caching for hashed assets (js, css).

- **Apache**:
  Create or update .htaccess:
  
  ```apacheconf
  RewriteEngine On
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule ^ /index.html [L]
  ```

Node.js / Express (simple example):

```js
const express = require('express');
const path = require('path');
const app = express();

app.use(express.static(path.join(__dirname, 'dist/your-project-name')));

app.get('/*', (req, res) => {
  res.sendFile(path.join(__dirname, 'dist/your-project-name/index.html'));
});

app.listen(8080);
```

### Popular Hosting Platforms

- **Firebase Hosting** → ng add @angular/fire then firebase deploy
- **Vercel** / **Netlify** → Drag & drop the dist/ folder or connect your Git repo
- **AWS S3 + CloudFront** or **Azure Static Web Apps**

## Additional Production Best Practices

- **HTTPS**: Always serve over HTTPS (use Let's Encrypt or your hosting provider's free SSL).
- **Compression**: Enable Gzip or Brotli on your server.
- **Caching**: Set aggressive caching for immutable assets (files with content hashes).
- **CDN**: Use a Content Delivery Network for faster global delivery.
- **Security**:
  - Set secure HTTP headers (CSP, HSTS, X-Frame-Options, etc.)
  - Keep dependencies updated (npm audit)
  - Use Subresource Integrity (SRI) when possible
- **Performance**:
  - Enable Server-Side Rendering (SSR) with Angular Universal if needed for SEO or faster initial load.
  - Monitor bundle size with ng build --stats-json + webpack-bundle-analyzer.
- **Monitoring & Analytics**: Integrate Google Analytics, Sentry, or New Relic.
- **CI/CD**: Automate builds and deployments using GitHub Actions, GitLab CI, Jenkins, etc.
- **Testing**: Run end-to-end tests in a production-like environment before going live.

## Quick Local Testing Checklist

```bash
# 1. Build for production
ng build --configuration production

# 2. Serve locally
http-server dist/your-project-name -p 8080 -c-1   # -c-1 disables caching
```

### MAINTENANCE

Maintaining a Spring Boot application involves a combination of tasks that help keep your application running smoothly, securely, and efficiently over time. Here's a comprehensive guide on how to maintain your Spring Boot application effectively:

### 1. **Regular Updates and Maintenance:**

- **Keep Dependencies Up-to-Date:** Regularly update your project dependencies, including Spring Boot, libraries, and frameworks, to benefit from bug fixes, security patches, and new features.

- **Code Refactoring:** Periodically review your codebase for code smells, duplicate code, and areas for improvement. Refactor your code to improve readability, maintainability, and performance.

- **Review and Optimize Database Queries:** Review database queries and optimize them for performance. Use tools like Hibernate's query profiling or database monitoring tools.

- **Monitor Logs:** Continuously monitor application logs for errors, exceptions, and performance bottlenecks. Use logging frameworks like Logback or Log4j and integrate log aggregation tools.

### 2. **Security:**

- **Keep Security Libraries Updated:** Regularly update security-related libraries to patch vulnerabilities.

- **Vulnerability Scanning:** Perform regular vulnerability scans on your application and its dependencies. Use tools like OWASP Dependency-Check.

- **Security Testing:** Conduct security testing, including penetration testing, to identify vulnerabilities in your application.

- **Implement Security Best Practices:** Follow security best practices such as input validation, output encoding, proper authentication, and authorization mechanisms.

### 3. **Monitoring and Performance:**

- **Application Performance Monitoring (APM):** Use APM tools like New Relic, AppDynamics, or Prometheus to monitor application performance, identify bottlenecks, and optimize code.

- **Metrics and Analytics:** Implement metrics and monitoring for key application metrics such as response times, error rates, and resource utilization.

- **Load Testing:** Conduct load testing to assess your application's performance under various user loads.

### 4. **Backup and Disaster Recovery:**

- **Regular Backups:** Implement a regular backup strategy for both your application files and your database.

- **Disaster Recovery Plan:** Develop a disaster recovery plan that outlines steps to take in case of unexpected failures or data loss.

### 5. **Continuous Integration and Deployment (CI/CD):**

- **Automated Testing:** Implement automated unit tests, integration tests, and end-to-end tests as part of your CI/CD pipeline.

- **Continuous Integration:** Set up a CI/CD pipeline to automate testing, building, and deploying your application.

- **Continuous Deployment:** Automate deployment to different environments using CI/CD practices.

### 6. **Documentation:**

- **Documentation Maintenance:** Keep your application's documentation up-to-date, including installation instructions, usage guidelines, and API documentation.

- **Change Logs:** Maintain detailed change logs to keep track of feature additions, bug fixes, and improvements.

### 7. **Scalability:**

- **Auto-scaling:** Design your application to handle increased loads by utilizing auto-scaling mechanisms.

- **Load Balancing:** Implement load balancing to distribute traffic evenly among multiple instances of your application.

### 8. **Regular Testing:**

- **Regression Testing:** Continuously perform regression testing to ensure that new changes do not break existing functionality.

- **User Acceptance Testing:** Conduct user acceptance testing to involve stakeholders and ensure the application meets their requirements.

### 9. **User Feedback:**

- **Collect Feedback:** Encourage users to provide feedback and report issues. Actively address user concerns and prioritize improvements.

### 10. **Version Control and Git:**

- **Version Control:** Use version control systems like Git to track changes, collaborate with your team, and manage code history.

### 11. **Employee Knowledge:**

- **Knowledge Sharing:** Maintain documentation and conduct knowledge-sharing sessions to ensure team members are aware of application intricacies
